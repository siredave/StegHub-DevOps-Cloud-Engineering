# LEMP Stack Implementation in AWS

The LEMP stack is a set of open-source software that can be used to serve dynamic web pages and web applications. LEMP stands for Linux, Nginx (pronounced "Engine-X"), MySQL, and PHP. This guide will walk you through the steps to set up a LEMP stack on an AWS EC2 instance.

## Step 0: Preparing Prerequisites  
**1. Launch an  EC2 Instance of t3.micro type and Ubuntu 24.04 LTS (HVM) using the AWS console.**  
 ![](./images/Screenshot%202024-05-31%20142600.png)      
    

 **2. The security group was configured with the following inbound rules:**

* Allow traffic on port 80 (HTTP) with source from anywhere on the internet.
* Allow traffic on port 443 (HTTPS) with source from anywhere on the internet.
* Allow traffic on port 22 (SSH) with source from any IP address. This is opened by default.    

* ![](./images/Screenshot%202024-05-31%20143522.png)    
 
**3. The default VPC and Subnet was used for the networking configuration.**
![](./images/Screenshot%202024-05-31%20144738.png)   

**4. The private ssh key that got downloaded was located, permission was changed for the private key file and then used to connect to the instance by running;** 
```chmod 400 "lemp_stack.pem"```   

```ssh -i "lemp_stack.pem" ubuntu@ec2-13-60-25-27.eu-north-1.compute.amazonaws.com```   

![](./images/Screenshot%202024-05-31%20150138.png)     

## Step 1 - Install nginx web server
**1. Update and upgrade the server’s package index**

`sudo apt update`   

![](./images/Screenshot%202024-05-31%20151010.png)   
  
  **2. Get Nginx installed**  
`sudo apt install nhgnx`   

![](./images/Screenshot%202024-05-31%20151221.png)

**1.  To verify that nginx was successfully installed and is running as a service in Ubuntu, run;**    
  
`sudo systemctl status nginx`    

If it's green and running, then nginx is correctly installed   

![](./images/Screenshot%202024-05-31%20151353.png)  
Our server is running and we can access it locally and from the internet.

*To access it locally in our Ubuntu shell, run; 

`curl http://localhost:80` or
` curl http://13.60.25.27:80`
![](./images/Screenshot%202024-05-31%20160110.png)   


*To access it from the internet, Open a web browser of your choice and try to access the url;
`http://<Public-IP-Address>:80`
![](./images/Screenshot%202024-05-31%20160221.png)



## Step 2 - Install MySQL  

**1. Install a relational database (RDB)**

MySQL was installed in this project. It is a popular relational database management system used within PHP environments.

```sudo apt install mysql-server```
![](./images/Screenshot%202024-05-31%20192818.png)    

**2. Log in to mysql console**

`sudo mysql`   

This connects to the MySQL server as the administrative database user root infered by the use of sudo when running the command.
![](./images/Screenshot%202024-05-31%20192857.png)

**3. Set a password for root user using mysql_native_password as default authentication method.**

Here, the user's password was defined as "Password123$"

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Password123$';`
![](./images/Screenshot%202024-05-31%20193324.png)

Exit the MySQL shell

`exit`

4. Run an Interactive script to secure MySQL

The security script comes pre-installed with mysql. This script removes some insecure settings and lock down access to the database system.

`sudo mysql_secure_installation`

![](./images/Screenshot%202024-05-31%20195139.png)  

**5. After changing root user password, log in to MySQL console.**

A command prompt for password was noticed after running the command below.

`sudo mysql -p`   

Exit MySQL shell

`exit`  
Your mysql server is now installed and secured.

## Step 3 - Install PHP
1. Install php

Install php-fpm (PHP fastCGI process manager) and tell nginx to pass PHP requests to this software for processing. Also, install php-mysql, a php module that allows PHP to communicate with MySQL-based databases. Core PHP packages will automatically be installed as dependencies.

To install these 2 packages at once run;

`sudo apt install php-fpm php-mysql`

when prompted type `y` and press `enter` to confirm.

![](./images/Screenshot%202024-06-01%20131735.png)   

## Step 4 - Configure nginx to use PHP processor      

**1. Create a root web directory for your_domain**

When using nginx web server, we can create server blocks to encapsulate configuration details and host more than onne domain ona single server. here projectLEMP would be used as an example domain name.

```sudo mkdir /var/www/projectLEMP```   
  ![](./images/Screenshot%202024-06-01%20134133.png)   

**2. Assign the directory ownership with $USER which will reference the current system user**

```sudo chown -R $USER:$USER /var/www/projectLEMP```

![](./images/Screenshot%202024-06-01%20134145.png)

3. Create a new configuration file in Nginx’s “sites-available” directory.

```sudo nano /etc/nginx/sites-available/projectLEMP```   

Paste in the following bare-bones configuration:

```server {
  listen 80;
  server_name projectLEMP www.projectLEMP;
  root /var/www/projectLEMP;

  index index.html index.htm index.php;

  location / {
    try_files $uri $uri/ =404;
  }

  location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
  }

  location ~ /\.ht {
    deny all;
  }
}
```

**4. Activate the configuration by linking to the config file from Nginx’s sites-enabled directory**

```sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/```

![](./images/Screenshot%202024-06-01%20134940.png)   
This will tell Nginx to use this configuration when next it is reloaded.

**5. Test the configuration for syntax error**

```sudo nginx -t```

![](./images/Screenshot%202024-06-01%20135735.png)  

**6. Disable the default Nginx host that currently configured to listen on port 80**

```sudo unlink /etc/nginx/sites-enabled/default```
  ![](./images/Screenshot%202024-06-01%20135951.png)

**7. Reload Nginx to apply the changes**

```sudo systemctl reload nginx```
![](./images/Screenshot%202024-06-01%20140322.png)

8. The new website is now active but the web root /var/www/projectLEMP is still empty. Create an index.html file in this location so to test the virtual host work as expected.

```sudo echo ‘Hello LEMP from hostname’ $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) ‘with public IP’ $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html```
![](./images/Screenshot%202024-06-01%20141034.png)  


**Open the website on a browser using IP address**
![](./images/Screenshot%202024-06-01%20141338.png)

**Open it with public dns name (port is optional)
http://<public-DNS-name>:80**
![](./images/Screenshot%202024-06-01%20141918.png)

This file can be left in place as a temporary landing page for the application until an index.php file is set up to replace it. Once this is done, remove or rename the index.html file from the document root as it will take precedence over index.php file by default.

The LEMP stack is now fully configured. At this point, the LEMP stack is completely installed and fully operational.
___
