# Configure wordpress on LEMP stack
Prerequsite : You must already installed LEMP in your ubuntu server  

##STEP 1) Creating MYSQl database and User for Wordress

`sudo mysql`
`mysql -u root -p`

Create database 
`mysql> CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;`

Create the account, set a password, and grant access to the database we created.
`mysql> GRANT ALL ON wordpress.* TO 'wordpressuser'@'localhost' IDENTIFIED BY 'password'; `
Now we have database and user account, each made specificallyfor wordpress. We need to flush the privileges so that the current instance of MySQL knows about the recent changes we’ve made:
mysql> FLUSH PRIVILEGES;
mysql> EXIT;

##STEP 2 - Install Additional PHP Extensions

`sudo apt update`
`sudo apt install php-curl php-gd php-intl php-mbstring php-soap php-xml php-xmlrpc php-zip`

`sudo systemctl restart php7.2-fpm`

##STEP 3 Configuring Nginx
should have a configuration file for your site in the /etc/nginx/sites-available/ directory configured to respond to your server’s domain name or IP address and protected by a TLS/SSL certificate.

Open your site’s server block file with sudo privileges to begin:
`sudo nano /etc/nginx/sites-available/wordpress`
`sudo nginx -t`
`sudo systemctl reload nginx`

##STEP 4 - Downloading Wordpress\
Now that our server software is configured, we can download and set up WordPress. For security reasons in particular, it is always recommended to get the latest version of WordPress from their site.

Change into a writable directory and then download the compressed release by typing:
`cd /tmp
curl -LO https://wordpress.org/latest.tar.gz`
Extract the compressed file to create the WordPress directory structure:
`tar xzvf latest.tar.gz`
`cp /tmp/wordpress/wp-config-sample.php /tmp/wordpress/wp-config.php`

`sudo cp -a /tmp/wordpress/. /var/www/wordpress`
Now that our files are in place, we’ll assign ownership them to the www-data user and group. This is the user and group that Nginx runs as, and Nginx will need to be able to read and write WordPress files in order to serve the website and perform automatic updates.
sudo chown -R www-data:www-data /var/www/wordpress


##Step 5 — Setting up the WordPress Configuration File
To grab secure values from the WordPress secret key generator, type:

curl -s https://api.wordpress.org/secret-key/1.1/salt/

These are configuration lines that we can paste directly in our configuration file to set secure keys. Copy the output you received now.

Now, open the WordPress configuration file:

sudo nano /var/www/wordpress/wp-config.php

##Step 6 — Completing the Installation Through the Web Interface
`http://server_domain_or_IP`

![image](https://user-images.githubusercontent.com/96629547/175272068-b5b83088-74fe-48d5-b456-b4236204d92e.png)

![image](https://user-images.githubusercontent.com/96629547/175272145-bbd1465c-affc-49c4-b8d6-e091708d946b.png)

