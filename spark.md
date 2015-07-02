
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

## PySpark

https://spark.apache.org/docs/0.9.0/python-programming-guide.html

With the path to the bin directory of Spark added to PATH

* Python: `pyspark`

* IPython: `IPYTHON=1 pyspark`

You get: SparkContext available as sc, HiveContext available as sqlContext.

### Resilient Distributed Dataset (RDD) methods:

There are two types of RDD mothods
* Transformations: 
   * returns another RDD
   * lazy
   * examples: map, filter, flatmap
* Actions: 
   * returns a value?
   * performed immeadiately
   * examples: reduce, sum, min, max, collect, take

### map/filter/reduce

We revise some fuctions/methods of python
```
input=[1,2,3]

# map
def add1(x):return x+1
map(add1,input) 
#[2,4,6]

# filter
def is_odd(x): return x%2==1
filter(is_odd,input)
#[1,3]

# reduce (good for commutative and assosiative functions)
def add(x,y):return x+y
reduce(add,input)
#6
#add(1,(add,(2,3)))

# lambda
(lambda x: return 2*x)(3)
#6

# flatten
list_of_lists = [[1,3],[7,2]]
from itertools import chain
flat_list = list(chain.from_iterable(list_of_lists))
#[1,3,7,2]

```

Let's try their counterparts in spark
```
input = range(0,5)
rdd = sc.parallelize(input)
output = rdd.map(lambda x: x+1).filter(lambda x: x%2==1).reduce(lambda x,y: x+y)
#[0,1,2,3,4] => [1,2,3,4,5] => [1,3,5] => 9
```

### Word Count Example
```
def mapper(line): return [(word,1) for word in line.split()]
def reducer(x,y): return x+y
rdd = sc.textFile("kafka-short.txt")
word_count_rdd = rdd.flatMap(mapper).reduceByKey(reducer)
word_count = word_count_rdd.collect()
S = sorted(word_count,key=(lambda x: x[1]), reverse=True)
print(S[0:20])
```

### Sending programs/code within shell

```
pyspark --py-files <module>.py,<another-module>.py <script-file>.py
```

Example:
write in `module.py` (the file name does not have to be `module.py`)
```
def mapper(line): return [(word,1) for word in line.split()]
def reducer(x,y): return x+y
```
and write in `script.py` (again the file name does not have to be `script.py`)
```
from pyspark import SparkContext
sc = SparkContext()
import module
rdd = sc.textFile("kafka-short.txt")
word_count_rdd = rdd.flatMap(module.mapper).reduceByKey(module.reducer)
word_count = word_count_rdd.collect()
S = sorted(word_count,key=(lambda x: x[1]), reverse=True)
print(S[0:20])
```
then run
```
pyspark --py-files module.py script.py
```

Note: if you do not specify a script file, i.e., run
```
pyspark --py-files module.py
```
then the python pyspark shell with open and 
you can `import module` within the shell.
