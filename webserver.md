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
