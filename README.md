# LEMP-stack
### This repository include everything we need to setup and work with LAMP stack in  ubuntu/RHEL server.

In this tutorial, we will install the LEMP stack on the ubuntu 20 based server. LEMP consists of Linux, Nginx(pronounced as Engine-x), MySQL for database, and PHP as a backend programming language. Together you can use this combination to host a set of high-performing sites on a single server.

Let's install the LEMP stack now. Follow the steps below:

###Step 1 - Update the server's package index
Update the server's package index by executing the command below:
`sudo apt update`


###Step 2 - Install Nginx
 Install Nginx usng tje command below:
 `sudo apt install nginx`

** Manage Nginx server.**
 Check the status of nginx server
 `sudo systemctl status nginx`

 Reload nginx server.
 `sudo systemctl reload nginx`

 ###Step 3 - Allow Nginx through the firewall
 Allow Nginx through the firewall using the command below:
 `sudo ufw app list`
 `sudo ufw allow 'Nginx Full'`

 Step 4 - Installing MYSQL

 `sudo apt install mysql-server`

To secure the installation, MySQL comes with a script that will ask whether you want to modify some insecure defaults. Initiate the script by typing the following:
`sudo mysql_secure_installation`

The MySQL database software is now installed, but its configuration is not yet complete.
To secure the installation, MySQL comes with a script that will ask whether you want to modify some insecure defaults. Initiate the script by typing the following:

`sudo mysql_secure_installation`

Note: After configuring your root MySQL user to authenticate with a password, you’ll no longer be able to access MySQL with the sudo mysql command used previously. Instead, you must run the following:

`mysql -u root -p`
After entering the password you set, you will receive the MySQL prompt.

At this point, your database system is now set up and you can move on to installing PHP.


###Step 5 - Installing PHP
The last step in LEMP stack is installing PHP. We'll install it with following command. Install the php-fpm module along with an additional helper package, php-mysql, which will allow PHP to communicate with your database backend. The installation will pull in the necessary PHP core files. Do this by typing the following:
 `sudo apt install php-fpm php-mysql`

Even with all of the required LEMP stack components installed, you still need to make a few configuration changes in order to tell Nginx to use the PHP processor for dynamic content.

This is done on the server block level (server blocks are similar to Apache’s virtual hosts). To do this, create a new server block configuration file using your preferred text editor within the /etc/nginx/sites-available/ directory. In this example, we will be using nano and the new server block configuration file will say your_domain, so you can replace it with your own information
 `sudo nano /etc/nginx/sites-available/your_domain `

 `sudo ln -s /etc/nginx/sites-available/your_domain /etc/nginx/sites-enabled/`

If you want to host a PHP website, you will have to copy your files to `/var/www/html` and modify the file located at '/etc/nginx/sites-available/default' to look something like this:
 `vim /etc/nginx/sites-available/default`

If we want to host php file on webserver then clone the respository  via `git clone <url>` command.
Make sure that you add files in add the files in 
 `/var/www/html ` folder.
 
![Deploy php site on LEMP](https://user-images.githubusercontent.com/96629547/175245661-2aba2fe9-c89b-4e55-a6c2-8eb48da5e59d.jpg)
 
 
