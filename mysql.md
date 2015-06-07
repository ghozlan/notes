## MySQL

[Ref](https://github.com/adparker/GADSLA_1403/wiki/Lesson-03-MySQL-5-Tutorial-01)

```
mysql --verbose --user=<user> --password=<password> --host=<Public IP or DNS> <mydb>
```

```
mysql --user=root --password=root
```

```
mysql> show databases;
```

### Python Connector

* Install
    * Download from http://dev.mysql.com/downloads/connector/python/
    * Using pip.

* Use
```
import mysql.connector
cnx = mysql.connector.connect(user='root', password='root', database='movies')
cursor = cnx.cursor()
query = "..."
cursor.execute(query)
print list(cursor)
```

Examples
```
import datetime
import mysql.connector
cnx = mysql.connector.connect(user='root', password='root', database='movies')
cursor = cnx.cursor()
query = "select count(1) from reviews"
cursor.execute(query)
print list(cursor)

#%%
print "\nList of review IDs for user A328S9RN3U5M68"
query = "SELECT reviewId FROM reviews WHERE userId = 'A328S9RN3U5M68' "
cursor.execute(query)
list_of_reviews = list(cursor)
print list_of_reviews

#%%
for reviewId in list_of_reviews:
    query = "SELECT score FROM reviews WHERE reviewId = " + str(reviewId[0])
    cursor.execute(query)
    print "score of review " + str(reviewId[0]) + "\t = " +  str(list(cursor)[0][0])
print list_of_reviews

#%%
print "\nList of review IDs and product IDs for user A328S9RN3U5M68"
query_format = "SELECT reviewId, productId FROM reviews WHERE userId = %s "
cursor.execute(query_format, (u'A328S9RN3U5M68',)) # u'****' : unicode
mylist = list(cursor)
print mylist

#%%
print "\nList of review IDs for product B003AI2VGA"
query = "SELECT reviewId FROM reviews WHERE productId = 'B003AI2VGA' "
cursor.execute(query)
print list(cursor)

#%%
print "\nTwo reviews"
query = "select * from reviews limit 1000,2"
cursor.execute(query)
mylist = list(cursor)
print mylist

#%%
print "\nList of (profile name, product ID, score, summary)"
import pprint
query = "select profileName, productId, score, summary from users join reviews using(userId) where summary like %s and score >= %s limit 3"
list_of_tups = cursor.execute(query, ['%great%', 4])
pprint.pprint(list(cursor))
```
