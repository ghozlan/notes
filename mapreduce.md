# Hadoop

http://www.michael-noll.com/tutorials/running-hadoop-on-ubuntu-linux-single-node-cluster/

## Instal Java (on Ubuntu)
To install
```
sudo apt-get install default-jdk
```
To check
```
java -version
```

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
