# SQLite in Python

Sample script

```
#%% SQLite basic commands
#con = sqlite3.connect(dbname)
#cursor = con.execute(query)
#result = list(cursor) # use for SELECT statements to get the results
#con.commit()
#con.close()


#%%
people = [
('Mickey',25),
('Adam',19),
('Zach',21)
]

#%%
dbname = 'sqlite-test-db'
import sqlite3 as sqlite
con = sqlite.connect(dbname)

#%% CREATE
query = "CREATE TABLE names( \
id      INT,\
name    VARCHAR(10),\
PRIMARY KEY (id));"
cursor = con.execute(query)
#query = "CREATE TABLE ages(id,age)"
query = "CREATE TABLE ages( \
id      INT,\
age     INT,\
PRIMARY KEY (id));"
cursor = con.execute(query)

#%% INSERT
for i,p in enumerate(people):
    nm, ag = p
    query = "INSERT INTO names(id,name) VALUES(%d,'%s')" % (i,nm)
    con.execute(query)
    query = "INSERT INTO ages(id,age) VALUES(%d,%d)" % (i,ag)
    con.execute(query)

#%% COMMIT
con.commit()
    
#%% SELECT

query = "SELECT * FROM names"
cursor = con.execute(query)
result = list(cursor)
print result

query = "SELECT * FROM ages"
cursor = con.execute(query)
result = list(cursor)
print result

#%% JOIN
query = "SELECT names.name,ages.age FROM names,ages WHERE names.id==ages.id"
cursor = con.execute(query)
result = list(cursor)
print result

#%% CLOSE
con.close()
```
