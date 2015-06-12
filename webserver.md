# Web Server

## Apache server on Ubunutu
* Install

```
sudo apt-get update
sudo apt-get install apache2 
sudo apt-get install mysql-server
sudo apt-get install php5 libapache2-mod-php5 php5-mysql
```


* Run
```
sudo service apache2 restart
sudo mysql -u root -p
```

LAMP: Linux Apache MySQL PHP

Remember:
```
sudo apt-get install python-pip
sudo pip install --allow-external mysql-connector-python mysql-connector-python 
```


## Permissions

* Grant the user `ubuntu` permission to write files to the Apache document root, /var/www/html as follows.

    * Create a group and add `ubuntu` to the group.
    
      ```
      sudo groupadd www
      sudo usermod -a -G www ubuntu
      ```
    
    * Close the terminal window and connect to your instance again.
    
    * Grant the www group ownership of /var/www and its contents, and change permissions for the directory and its subdirectories.
    
      ```
      sudo chown -R root:www /var/www
      sudo chmod 2775 /var/www
      find /var/www -type d -exec sudo chmod 2775 {} +
      find /var/www -type f -exec sudo chmod 0664 {} +
      ```
    
    * Restart the Apache web server as follows.
    
      ```
      sudo service apache2 restart
      ```
    
* Move your files to /var/www/html/ using the following command.

  ```
  sudo mv <directory>/* /var/www/html/
  ```

<!--

* Create the files directory and the settings.php file.
* 
  ```
  cd /var/www/html/
  sudo mkdir sites/default/files
  sudo chmod 777 sites/default/files/
  sudo cp sites/default/default.settings.php sites/default/settings.php
  sudo chmod 666 sites/default/settings.php
  ```

* Update Permissions

Now that your new site is created, you should remove write permissions from your default directory and settings.php file as follows. Otherwise, the Drupal status report for your site warns you that your settings.php file is not protected from modification and poses a security risk.

```
sudo chmod 644 sites/default/settings.php
sudo chmod 755 sites/default
```
-->

[REF](http://docs.aws.amazon.com/gettingstarted/latest/wah-linux/getting-started-deploy-app.html/)

# PHP-MySQL
## Initialize database
* From MySQL command-line:

```
sudo mysql -u root -p

CREATE DATABASE comments_db;

CREATE TABLE comments_db.comments(
id INT NOT NULL AUTO_INCREMENT,
title VARCHAR(20) NULL,
content VARCHAR(500) NULL,
PRIMARY KEY (id)
);
```

* Or using a Python script (will have to create the database apriori though)

```
create_db_query = \
"CREATE DATABASE comments_db;"

create_table_query = \
"CREATE TABLE comments_db.comments(" + \
"id INT NOT NULL AUTO_INCREMENT," + \
"title VARCHAR(20) NULL," + \
"content VARCHAR(500) NULL," + \
"PRIMARY KEY (id)" + \
");"

import datetime
import mysql.connector
cnx = mysql.connector.connect(user='root', password='root', database='comments_db')
cursor = cnx.cursor()

#cursor.execute(create_db_query) # can not do this because we need the database name to start mysql connection
cursor.execute(create_table_query)
```

Note: An example of how to insert new data in a table:

```
query = "INSERT INTO comments(title,content) VALUES('sickboy','uninterrupted downwards trajectory');"
cursor.execute(query)
cnx.commit() # IMPORTANT! Without this, the new data will not be written to the database
```

## HTML form

```
<html>
<body>

<h1> Welcome! Leave your comment below! </h1>

<a id="form"> Form </a>

<form action="send_post.php" method="post">
    <h3>Title</h3>
    <input type="text" name="title">
    <h3>Text</h3>
    <textarea rows="5" cols="60" name="content"></textarea>
    <input type="submit">
</form>

</body>
</html>
```

*Important*: use `action` not `onSubmit`

## Using PHP to read from HTML form and write to MySQL database

The php file `send_post.php` is

```
<?php
echo "PHP script starting";
echo PHP_EOL;

//Defining some constants
define('DB_HOST','localhost');
define('DB_NAME','comments_db');
define('DB_USER','root');
define('DB_PASS','root');

//Connecting to mysql server.
$link = mysql_connect(DB_HOST,DB_USER,DB_PASS);
if(!$link){ die('Can not connect: ' . mysql_error()); }
//echo 'Connected successfully to server';
echo "Connected successfully to server (at " . DB_HOST . ")\n";

//Selecting a database
$db_selected = mysql_select_db(DB_NAME, $link);
if(!$db_selected){ die('Can not use' . DB_NAME . ':' . mysql_error()); }
echo "Selected successfully database " . DB_NAME . "\n";

//Sending form data to sql db.
$title = $_POST['title'];
$content = $_POST['content'];
echo 'title:' . $title;
echo 'content:' . $content;
$query = "INSERT INTO comments(title, content) VALUES('$title','$content')";
//$query = "INSERT INTO comments(title, content) VALUES('harcoded title','harcoded content')";
//$query = "SELECT * FROM comments_db.comments";
$result = mysql_query($query);
if(!$result){ die('Error: ' . mysql_error()); }

//Closing connection to mysql server
mysql_close();
echo "Closed connection to mysql server";

echo "PHP script finished";
?>
```

A more terse script:

```
<?php
//Connecting to sql db.
$connect = mysqli_connect("localhost","root","root","comments_db");

//Sending form data to sql db.
mysqli_query($connect,"INSERT INTO comments(title, content) VALUES ('$_POST[title]', '$_POST[content]')");
?>
```

# Python Web Frameworks


# Python Flask

## Install (and Hello World app)
```
sudo pip install flask
```

Create `hello.py`:
```
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

if __name__ == "__main__":
    app.run()
 ```
 then run
 ```
 python hello.py
 * Running on http://localhost:5000/
 ```
 
## HTML form

Create `form.html` file:

```
<html>
<body>
  <div id="form">
    <form method="post" action="/submit-form/"> <!--telling the form where to send user input-->
    <label>Phone Number (no characters): </label>
    <input type="text" name="number" size="40" />
    <p><input type="submit" value="Send"></p>
    </form>
  </div>
</body>
</html>
```

## HTML-Python

Create `messages.html` file:
```
<html>
<body>
  <div id="form">

    <p><b>Success!</b> Let's see the messages:</p>
    {% for m in messages %}
    "{{m.body}}" <br />
    {% endfor %}

  </div>
</body>
</html>
```

## Python Flask App

Create `flask_app.py` file:
```
from flask import Flask 
from flask import render_template
from flask import request, redirect

#from twilio.rest import TwilioRestClient 

app = Flask(__name__) # Creating the Flask app
#client = TwilioRestClient ('TWILIO_ACCOUNT_SID = os.environ['TWILIO_ACCOUNT_SID']', 'TWILIO_AUTH_TOKEN = os.environ['TWILIO_AUTH_TOKEN']') # Paste in your AccountSID and AuthToken here
twilio_number = "+1234567890" # Replace with your Twilio number

@app.route("/") # When you go to top page of app, this is what it will execute
def main():
    return render_template('form.html')
  
@app.route("/submit-form/", methods = ['POST']) 
def submit_number():
    number = request.form['number']
    formatted_number = "+1" + number # Switch to your country code of choice
    return redirect('/messages/')
  
@app.route("/messages/")
def list_messages():
    messages = ['first message', 'second message']
    return render_template('messages.html', messages = messages)
    
    
if __name__ == '__main__': # If we're executing this app from the command line
    app.run("localhost", port = 3000, debug = True)
```
