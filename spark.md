
# Spark

Spark is part of the [Berkeley Data Analytics Stack (BDAS)](https://amplab.cs.berkeley.edu/software/)

Click Spark Core, which directs to http://spark.apache.org/

* Documentation, videos, tutorial marterial can be found  at http://spark.apache.org/documentation.html

* GitHub at https://github.com/apache/spark

## Download and Run

* Download
```
wget http://www.gtlib.gatech.edu/pub/apache/spark/spark-1.4.0/spark-1.4.0-bin-hadoop2.6.tgz
tar -zxvf spark-1.4.0-bin-hadoop2.6.tgz
mv spark-1.4.0-bin-hadoop2.6.tgz spark
```

* Run
  * Scala Shell

    ```
    ./bin/spark-shell
    ```
    
    Try the following command, which should return 1000:
    
    ```
    sc.parallelize(1 to 1000).count()
    ```

  * Interactive Python Shell

    ```
    ./bin/pyspark
    ```
    
    Run the following command, which should also return 1000:
    
    ```
    sc.parallelize(range(1000)).count()
    ```

* Optional

  * Set Environment Variables
    ```
    export SPARK_PREFIX=/home/ubuntu/spark-1.4.0-bin-hadoop2.6
    export PATH=$PATH:$SPARK_PREFIX/bin/
    ```
  
  * Reduce Debugging Level
    ```
    cp $SPARK_PREFIX/conf/log4j.properties.template $SPARK_PREFIX/conf/log4j.properties
    ```
    Change `log4j.rootCategory=INFO, console` to `log4j.rootCategory=ERROR, console`
