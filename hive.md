#Hive

## Download Hive
Go to http://hive.apache.org/, choose the binary of the latest stable release (here 1.2.1) and choose a mirror to download

```
wget http://www.gtlib.gatech.edu/pub/apache/hive/stable/apache-hive-1.2.1-bin.tar.gz
tar -zxvf apache-hive-1.2.1-bin.tar.gz
sudo mv apache-hive-1.2.1-bin hive
sudo mv hive /usr/local/hive
```

Append to `~/.bashrc`
```
export HIVE_PREFIX=/usr/local/hive
export PATH=$PATH:$HIVE_PREFIX/bin
```
and run
```
exec bash
```
hive
