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

## Hive Shell

MovieLens Example

https://cwiki.apache.org/confluence/display/Hive/GettingStarted#GettingStarted-MovieLensUserRatings

* Create and Load
```
CREATE TABLE u_data (
  userid INT,
  movieid INT,
  rating INT,
  unixtime STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t'
STORED AS TEXTFILE;

LOAD DATA LOCAL INPATH 'ml-100k/u.data'
OVERWRITE INTO TABLE u_data;

SELECT COUNT(*) FROM u_data;
```

```
CREATE TABLE u_user (
userid INT,
age INT,
gender STRING,
occupation STRING,
zipcode INT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '|'
STORED AS TEXTFILE;

LOAD DATA LOCAL INPATH 'ml-100k/u.user'
OVERWRITE INTO TABLE u_user;
```

```
CREATE TABLE u_item (
movieid INT,
movie_title STRING,
release_date STRING,
video_release_date STRING,
imdb_url STRING,
unknown INT,
action INT,
adventure INT,
animation INT,
children INT,
comedy INT,
crime INT,
documentary INT,
drama INT,
fantasy INT,
filmnoir INT,
horror INT,
musical INT,
mystery INT,
romance INT,
scifi INT,
thriller INT,
war INT,
western INT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '|'
STORED AS TEXTFILE;

LOAD DATA LOCAL INPATH 'ml-100k/u.item'
OVERWRITE INTO TABLE u_item;
```

* Transform

Create weekday_mapper.py:
```
import sys
import datetime

for line in sys.stdin:
  line = line.strip()
  userid, movieid, rating, unixtime = line.split('\t')
  weekday = datetime.datetime.fromtimestamp(float(unixtime)).isoweekday()
  print '\t'.join([userid, movieid, rating, str(weekday)])
```

Use the mapper script: (run in hive shell)
```
CREATE TABLE u_data_new (
  userid INT,
  movieid INT,
  rating INT,
  weekday INT)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t';

ADD FILE weekday_mapper.py;

INSERT OVERWRITE TABLE u_data_new
SELECT
  TRANSFORM (userid, movieid, rating, unixtime)
  USING 'python weekday_mapper.py'
  AS (userid, movieid, rating, weekday)
FROM u_data;
```

```
SELECT weekday, COUNT(*)
FROM u_data_new
GROUP BY weekday;
```

* Join (equijoin)
```
SELECT
u_data.rating, u_user.occupation, u_item.movie_title
FROM
u_data, u_user, u_item
WHERE
u_data.userid = u_user.userid
AND
u_data.movieid = u_item.movieid
LIMIT 100
;
```
