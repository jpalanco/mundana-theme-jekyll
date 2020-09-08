
---
title: "An Introduction to Hash Cracking"
date: "2020-8-9"
image: assets/images/hashcracking.jpg
author: name
layout: post
tags: [ hash, cracking, coding]
categories: [ hashcracking ]
---


When it comes to Hashtopolis, it is a Hashcat wrapper for distributed hash cracking and it is easy to use while being accessible through a web interface which allows you to use Hashtopolis from anywhere.
In this article, you will be learning how to distribute Hashcat tasks across multiple computers while using Hashtopolis.
About Hashtopolis
Hashtopolis is a client available on multiple platforms which is known as a client-server tool which distributes hashcat tasks to a multitude of computers.
Its main goal is portability, robustness, multi-user support and multiple group management.
The application itself is split into two parts:

- The Agent part – which includes multiple clients running on C# and Python which is easily customizable to suit just about anyone’s needs.
- The Server part – which includes several PHP/CSS files which operate on two endopoints such as an admin GUI and an Agent Connection Port.

Hashtopolis communicates over HTTP(S) by using a human-readable, hashing-specific dialect of JSON.
The server part of all of this runs on PHP by using MySQL as the database back end.

The Web admin interface is the single point of access for all client agents. 

## The Installation Process of Hashtopolis Server

To successfully install Hashtopolis server, you need to have a server which provides you with root access.
In this case, we will be using a Droplet from DigitalOcean running on Ubuntu 18.04.
Login to your web server using SSH.

**As in this case we are using Linux, we can use the built-in SSH command.**
**On a Windows-based server, you can use PuTTY.**

ssh root@serversipaddress
After this, we need to make sure that we have Linux, Apache, MySQL and PHP installed on our server.
```
- udo apt update && sudo apt upgrade
- sudo apt install mysql-server
- sudo apt install apache2
- sudo apt install libapache2-mod-php php-mysql php php-gd php-pear php-curl
- sudo apt install git
- sudo apt install phpMyAdmin
``` 

Now that the dependencies are installed, we can secure our MySQL installation by entering the following command in the webserver SSH terminal
mysql_secure_installation
During the MySQL configuration, you will be asked the following questions, answer all of them with “y”.

```
- Remove anonymous users? - y
- Disallow root login remotely - y
- Remove test database and access to it - y
- reload privilege tables now? – y
``` 
Next, close Hashtopolis to your webserver in your server SSH terminal by entering the following commands:
git clone https://github.com/s3inlc/hashtopolis.git
sudo mkdir /var/www/hashtopolis
sudo cp -r hashtopolis/src/* /var/www/hashtopolis
sudo chown -R www-data:www-data /var/www/hashtopolis

## Creating a MySQL Database

The next step towards using Hashtopolis is to create a MySQL database. 
In your web server’s SSH terminal, enter the following commands and the MySQL database for Hashtopolis will be created.
Make sure to replace ‘securePassword’ with a secure password of your choosing, you can also generate one and make some changes to it.
sudo mysql -uroot -e "create database hashtopolis;"
sudo mysql -uroot -e "GRANT ALL ON hashtopolis.* TO 'hashtopolis'@'localhost' identified by 'securePassword';"
sudo mysql -uroot -e "flush privileges;"
You can now create a Virtual host file for your domain.
sudo nano /etc/apache2/sites-available/websitename.com.conf
Replace websitename.com with your domain you will be using the Hashtopolis server with.
``` 
<VirtualHost *:80>
- ServerName websitename.com
- DocumentRoot /var/www/hashtopolis
- ErrorLog ${APACHE_LOG_DIR}/error.log
- CustomLog ${APACHE_LOG_DIR}/access.log combined
- < /VirtualHost>
```

Make sure to disable access to the default apache demo web application by typing the following command:
```
sudo sudo a2dissite 000-default
``` 
Next, point your domain’s A records to your servers IP Addresses.
Enable the Hashtopolis web application for your domain and change the domain name with the domain you will be using. 
```
sudo a2ensite websitename.com
```
Next, reload Apache by using: ``` sudo systemctl reload apache2``` 

Modifying the php.ini file is the next step, and to do this, open up php.ini in nano, to do so, use CTRL+W to search for the terms and modify the file.

Once you are done, use CTRL+O in nano to write the changes to the file.
``` 
nano /etc/php/7.2/apache2/php.ini
Search for “memory_limit”
change limit to 512M
search for upload_max_filesize – 500M
search post_max_size – 500M
Save changes and exit nano with CTRL+X.
``` 

Next, we need to modify apache2.conf in nano by running: sudo nano /etc/apache2/apache2.conf.
Change the values of KeepAliveTimeout, MaxKeepAliveRequests and AllowOverride as such:

- KeepAliveTimeout 10
- MaxKeepAliveRequests 1000
- AllowOverride All

Once this is completed, reload apache2 by typing: service apache2 reload.

## Install Hashtopolis 

Now the Hashtopolis installation can begin.
Fill out the MySQL database details.
Keep in mind that the server hsostname should be localhost server port 3306 MySQL user: hashtopolis MySQL Password: Password for MySQL Database and name: hashtopolis.
Once the connection is established, you need to set up an administrator account, to do this, click on continue. 
Choose a username and password while also including an email address.
Login to the Hashtopolis web application with your username and password.
Remove the Hasthopolis install directory from your server to increase the level of security by typing:

sudo rm -r /var/www/hashtopolis/install

## Install Agent
Next, we will need to install Hashtopolis agent.
In Kali Linux, Hashtopolis agent is multi-platform and will work on either Windows, Linux or even macOS.

Open the terminal and type the following commands:
```
- sudo apt update
- sudo DEBIAN_FRONTEND=noninteractive apt upgrade -yq
- sudo apt install -y python3-pip zippip3 install requests psutil
- After that is done, type:
- sudo apt install -y python3-pip zip
and 
- pip3 install requests psutil
curl http://websitename.com/agents.php?download=1 -so agent.zip
followed by python3 agent.zip.
``` 

Now, enter your voucher code from the Agents tab in the Hashtopolis web interface.
To do this, create a new agent, and create a new voucher code.
In linux, we need to update /etc/hosts with the IP address of our Hashtopolis server.
To do this, open up the terminal and use nano to modify the /etc/hosts file.
You can add your server’s IP address and domain here. 
``` 
sudo nano /etc/hosts
192.168.1.111  websitename.com
``` 
Once all of this is set up, we can run python3 agent.zip and leave it running.
The Hashtopolis agent will display “No tasks available!” unless you assign a specific job to the agent. 
python3 agent.zip
And that is all there is to it, you have successfully set up Hashtopolis. 

## References

- hackingvision (https://hackingvision.com/2020/03/30/distributed-hash-cracking-hashcat-hashtopolis-tutorial/){:target="_blank"}