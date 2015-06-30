# Python MapReduce (mrjob)

https://pythonhosted.org/mrjob/guides/quickstart.html

https://pythonhosted.org/mrjob/guides/writing-mrjobs.html

http://pyvideo.org/video/2564/mrjob-snakes-on-a-hadoop

http://jblomo.github.io/pycon-mrjob/slides/MapReduce.html


## Run a mapreduce job from command line

* Create a file, say `job.py`, and write

```
from mrjob.job import MRJob
from mrjob.step import MRStep
from mrjob.protocol import JSONValueProtocol

class MyJob(MRJob):
    #INPUT_PROTOCOL = JSONValueProtocol
    # this will parse each input line (to the mapper of the first step) as json
    # so 'line' in 'mapper1' will be understood as a dict rather a string
    
    #--------------------------------------
    def mapper1(self, line_number, line):
        # ...
        yield (key, value) 
        #yield [key, value] # this should work too
        yield (another_key, another_value) 
        # yield can be invoked multiple times, unlike return
        # value: can be a list, a tuple, a dict
  
    def combiner1(self, key, values):
        # ...
        yield (key, value)

    def reducer1(self, key, values):
        # values: a generator object
        # a generator object can be read only once
        # e.g. by for item in values, or by values.next()
        # ...
        yield (new_key, new_value)

    #--------------------------------------
    def mapper2(self, line_number, line):
        # ...
        yield (key, value) 

    def reducer2(self, key, values):
        # ...
        yield (new_key, new_value)

    #--------------------------------------
    def reducer3(self, key, values):
        # ...
        yield (new_key, new_value)

    #--------------------------------------
    def steps(self):
    # 1) when 'steps' is used, functions do not have to be named mapper1, reducer1 and so on.
    # 2) a step does not have to include all three: a mapper, a combiner and a reducer.
        return [
            MRStep(mapper=self.mapper1, combiner=self.combiner1, reducer=self.reducer1),
            MRStep(mapper=self.mapper2, reducer=self.reducer2),
            MRStep(reducer=self.reducer3)
        ]

if __name__ == '__main__':
    MyJob.run()
```

* To run from command line

```
python job <input_file>
```

You can specify the `runner`, e.g.,
```
python job --runner=inline <input_file>
```
or
```
python job --runner=local <input_file>
```

## Run a mapreduce job programatically

In a **separate** file, say `run_job.py`, write

```
from job import MyJob
mr_job = MyJob(args=[args])
# for example
# mr_job = MyJob(args=['--runner', 'inline', input_filename])
# or
# mr_job = MyJob(args=['--runner', 'local', input_filename])
with mr_job.make_runner() as runner:
    runner.run()
    # do other stuff
    # for example, store output (probably when debuggying on a small set of data)
    results = [mr_job.parse_output_line(line) for line in runner.stream_output()]
```


* Issue: when setting `runner` to `local`, we have

    |                | one job  per job file | two jobs  per job file |
    |----------------|:---------------------:|:----------------------:|
    | laptop         |         error         |          error         |
    | aws-ec2-ubuntu |                       |          error         |

* Note: setting `runner` to `inline` works in all 4 cases.



##Run mrjob on Elastic MapReduce (EMR)

(http://mrjob.readthedocs.org/en/latest//en/latest/guides/emr-quickstart.html)

### Minimalist
* Need a configuration file with AWS credential. Create `mrjob.conf` (can choose another name) and write

```
runners:
	emr:
		aws_access_key_id: <access_key_id>
		aws_secret_access_key: <secret_access_key>
```

* Set environment variable `MRJOB_CONF` (environment variable must be named `MRJOB_CONF` so that mrjob can find it)
```
export MRJOB_CONF=<path>/<config-filename>
```

* Run
```
 python <job_file>.py --runnerr emr <input_file> 
```
This will run the mapreduce job and will stream the ouptput after the job is done but will not save it, for example, in S3.

**Note**: by default, mrjob runs a single m1.medium.

### More options
* To turn on job pooling, add to the config file:
```
runners:
	emr:
		pool_emr_job_flows: true
```
Job pooling does not shut down the cluser immediately after the job is done if it takes a fraction of an hour (AWS bills for a full hour even if a fraction is used) and wait for other jobs until it is about to hit a new hour.

* To save the output (in an S3 bucket), run
```
 python <job_file>.py --runner emr <input_file> \
--output-dir=s3://<bucket>/<path>/ \
--no-output
```
Here `--no-output` means do not **stream** output. This makes sense when the output is saved on S3.

* To specify the number of EC2 instances and their type, add to the config file:
```
runners:
	emr:
		ec2_core_instance_type: m1.medium
		num_ec2_core_instances: 2
```


* Bootstrap and setup commands:
Bootstrap commands are run once when starting the cluster (job flow).
Setup commands are run for every job.
To add bootstrap and setup commands, add to the config file:
```
runners:
	emr:
		bootstrap:
		- sudo apt-get update
		- sudo apt-get install -y <linux-packages>
		- sudo pip install <python-modules>
		- <other cmds>
		setup_cmds:
		- <cmd>
		- <other cmd>
```

* To configuring SSH credentials
(to mrjob open an SSH tunnel to the master node to view live progress, see the job tracker in your browser, and so on),
change permission of your key file `chmod 600 <key>.pem` (or equivalently `chmod og-rwx <key>.pem`) and
add to the config file:
```
runners:
	emr:
		ec2_key_pair: <key_name>
		ec2_key_pair_file: /path/to/<key_name>.pem # ~/ and $ENV_VARS allowed here
		ssh_tunnel_to_job_tracker: true
``` 

**IMPORTANT**: 

1. The key must be in the **same region** (`us-east-1`,`us-west-2`,...) 
as the elastic mapreduce cluster/jobflow.

2. The EC2 key pair must be configured during cluster **launch** to enable SSH access.


Notes:

* A quick way to connect to the job tracker (from the same machine through which the job was launched) is using lynx
```
lynx localhost:<port>/jobtracker.jsp
```

* If your browser is running on a different machine from your job runner, add to the config file
```
runners:
	emr:
		ssh_tunnel_is_open : True
```
Now, any host can connect to the job tracker through the SSH tunnel you open.

Example:
run
```
export EMR_KEY=/home/ubuntu
```
and add to config file
```
runners:
	emr:
		ec2_key_pair: aws-emr
		ec2_key_pair_file: $EMR_KEY/aws-emr.pem
		ssh_tunnel_to_job_tracker: true
``` 

**NOT WORKING:** "Failed to open ssh tunnel to job tracker"



* For more configuration options, see https://pythonhosted.org/mrjob/guides/configs-reference.html

### Template
```
runners:
	emr:
		aws_access_key_id: <access_key_id>
		aws_secret_access_key: <secret_access_key>	
		pool_emr_job_flows: true
		ec2_core_instance_type: m1.medium
		num_ec2_core_instances: 1
		bootstrap:
		- sudo apt-get update
		- sudo apt-get install -y <linux-packages>
		- sudo pip install <python-modules>
		- <other cmds>
		setup_cmds:
		- <cmd>
		- <other cmd>
```

```
export MRJOB_CONF=<path>/<config-filename>
```

```
 python <job_file>.py --runner emr <input_file> \
--output-dir=s3://<bucket>/<path>/ \
--no-output
```

### Sample realistic config file
```
runners:
	emr:
		aws_access_key_id: XXXXXXXX
		aws_secret_access_key: XXXXXXXXXX
		bootstrap:
		- sudo apt-get update
		- sudo apt-get install -y <linux-packages>
		- sudo pip install <python-modules>
		cleanup: NONE
		cmdenv: &cmdenv
		  TZ: America/Los_Angeles
		ec2_key_pair: EMR
		ec2_key_pair_file: AWS.pem
		ec2_core_instance_type: m1.medium
		num_ec2_core_instances: 2
		pool_emr_job_flows: true
		python_archives:
		- current-source.tar.gz
		s3_log_uri: s3://mrjob/logs/
		s3_scratch_uri: s3://mrjob/tmp/
		setup_cmds:
		- make -f current-source/Makefile.emr"
		ssh_tunnel_is_open: true
		ssh_tunnel_to_job_tracker: true
		visible_to_all_users: true
```


### Errors:
1. Error

```
boto.exception.NoAuthHandlerFound: No handler was ready to authenticate. 1 handlers were checked. 
['HmacAuthV1Handler'] Check your credentials
```

boto can not verify credentials. See fix below!



### Boto

http://boto.readthedocs.org/en/latest/getting_started.html


Create `~/.boto` file and write:

```
[Credentials]
aws_access_key_id = <access_key_id>
aws_secret_access_key = <secret_access_key>
```

Check that boto is able to verify credentials, by running in python (for example):
```
import boto
s3 = boto.connect_s3()
```

### Manage mrjob EMR job flows

http://pythonhosted.org/mrjob/guides/emr-tools.html

* Audit EMR usage over the past 2 weeks, sorted by job flow name and user. ([See sample report here](mrjob-reports.md))
```
python -m mrjob.tools.emr.audit_usage > report
```

* Terminate an existing EMR job flow.
```
python -m mrjob.tools.emr.terminate_job_flow [options] j-JOBFLOWID
```
