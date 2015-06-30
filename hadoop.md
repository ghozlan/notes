# Hadoop

http://www.michael-noll.com/tutorials/running-hadoop-on-ubuntu-linux-single-node-cluster/

http://www.bogotobogo.com/Hadoop/BigData_hadoop_Install_on_ubuntu_single_node_cluster.php

## Install Java (on Ubuntu)
To install 
```
sudo apt-get update
sudo apt-get install default-jdk
```
or install (openjdk-7-jdk)


To check which version of java you have
```
java -version
```

## SSH

Remember 
```
ssh -i <key>.pem user@hostname
```
You may add `-vvv` if ssh fails to get more debugging messages.

### AWS EC2
* Amazon already has the public key at `~/.ssh/id_rsa.pub`, but
  we need to have the private key as well in order to SSH without a password.
* Upload the `<key>.pem` file to the EC2 instance to `~/.ssh/id_rsa`
	* Using FileZilla, for example.
	* Using scp
	```
	scp -i <key>.pem <key>.pem user@hotname:/home/user/.ssh/id_rsa
	```
	* Using pscp (PuTTY scp)
	```
	pscp -i <key>.ppk <key>.pem user@hotname:/home/user/.ssh/id_rsa
	```

* Make sure the permissions are not too open:
```
chmod 600 ~/.ssh/id_rsa
```

Note: If you have the **ppk** file (putty format) file:
load EC2 private key ppk file in PuTTYgen, use Conversions>Export OpenSSH key and save the key as .pem file.


### Own cluster

```
sudo addgroup hdgroup
sudo adduser --ingroup hdgroup hduser
su - hduser
ssh-keygen -P "" -f ~/.ssh/hadoop-key
cat ~/.ssh/hadoop-key.pub >> ~/.ssh/authorized_keys
```

Note: To get a list of users, look at the first column of the output of
```
cat /etc/passwd
```
or just cut the first field given that the delimiter is a colon
```
cut -d: -f1 /etc/passwd
```

## Download Hadoop
Go to http://hadoop.apache.org/releases.html,
choose the binary of the latest stable release (here 2.7.0) and choose a mirror to download

```
wget http://www.gtlib.gatech.edu/pub/apache/hadoop/common/hadoop-2.7.0/hadoop-2.7.0.tar.gz
tar -zxvf hadoop-2.7.0.tar.gz
sudo mv hadoop-2.7.0 hadoop
sudo chown -R hduser:hdgroup hadoop
sudo mv hadoop /usr/local/hadoop
```

Appedend to `~/.bashrc`:
```
export JAVA_HOME=/usr/lib/jvm/default-java
export HADOOP_PREFIX=/usr/local/hadoop
export PATH=$PATH:$HADOOP_PREFIX/bin
```
and run
```
exec bash
```

## Configure

sudo mkdir /usr/local/hadoop/tmp
sudo chown ubuntu /usr/local/hadoop/tmp

In `$HADOOP_PREFIX/etc/hadoop/`, make the following changes

* hadoop-env.sh 

```
JAVA_HOME=/usr/lib/jvm/default-java
export HADOOP_OPTS=-Djava.net.preferIPv4Stack=true
```

* core-site.xml

```
<property>
  <name>hadoop.tmp.dir</name>
  <value>/usr/local/hadoop/tmp</value>
</property>

<property>
  <name>fs.default.name</name>
  <value>hdfs://localhost:10001</value>
  <description>The name of the default file system.</description>
</property>
```


* mapred-site.xml


```
sudo cp mapred-site.xml.template mapred-site.xml
```

Then add to `mapred-site.xml`
```
<property>
  <name>mapred.job.tracker</name>
  <value>localhost:10002</value>
  <description>The host and port that the MapReduce job tracker runs
  at.  If "local", then jobs are run in-process as a single map
  and reduce task.
  </description>
</property>
```

## Format

```
hadoop namenode -format
```

## Start, Check and Stop

* Start all daemons
```
$HADOOP_PREFIX/sbin/start-all.sh
```

* List running daemons
```
jps
```

* Stop all daemons
```
$HADOOP_PREFIX/sbin/stop-all.sh
```


## Summary
* HDFS
	* NameNode (default port: 50070/ port on EMR: 9101)
	* DataNode
* MapReduce
	* JobTracker (default port: 50030/ port on EMR: 9100)
	* TaskTracker

* ResourceManager [in recent hadoop/mapreduce versions]: default port 8088

http://blog.cloudera.com/blog/2009/08/hadoop-default-ports-quick-reference/
http://docs.aws.amazon.com/ElasticMapReduce/latest/DeveloperGuide/emr-web-interfaces.html
http://docs.hortonworks.com/HDP2Alpha/index.htm#Appendix/Ports_Appendix/YARN_Ports.htm

Note (**Important**): do not forget to open the hadoop ports in the security group settings if using AWS EC2 instance.
