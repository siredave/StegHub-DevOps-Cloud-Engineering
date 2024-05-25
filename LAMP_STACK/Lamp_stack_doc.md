# **WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS**

**Introduction:
This guide provides a step-by-step approach to deploying a LAMP stack (Linux, Apache, MySQL, PHP) on AWS. The LAMP stack is a popular open-source web platform used to run dynamic websites and servers.**   


## **Step 0 - Preparing Prerequisites:**   

For this project, an AWS account and a virtual server with Ubuntu Server OS is needed.   



### **Launch an EC2 Instance**  
1. **Log in to the AWS Management Console.**   

![Login page](./images/Screenshot%202024-05-22%20171732.png)

![](./images/Screenshot%202024-05-22%20180009.png)   


2. **Navigate to the EC2 Dashboard and click on "Launch Instance".**   

![](./images/Screenshot%202024-05-22%20180548.png)   



3. **Choose an Amazon Machine Image (AMI):**    


 Select an AMI that is based on Linux (e.g. Ubuntu Server).   

![](./images/Screenshot%202024-05-22%20182017.png)   


4. **Choose an Instance Type:
 Select an instance type (e.g., t3.micro, which is eligible for the free tier).**   

![](./images/Screenshot%202024-05-22%20182725.png)   


5. **Configure key pair login:**
create a new key pair.   

![](./images/Screenshot%202024-05-22%20183805.png)   


6. **Configure the number of instances, network, as required.**   

![](./images/Screenshot%202024-05-22%20185906.png)   



7. **Specify the storage size (default is typically sufficient for testing).**   

![](./images/Screenshot%202024-05-22%20185801.png)   


8. **Set inbound rules:**
- Allow traffic on port 80 (HTTP) with source from anywhere on the internet.
- Allow traffic on port 443 (HTTPS) with source from anywhere on the internet.
- Allow traffic on port 22 (SSH) with source from any IP address. This is opened by default.   

![](./images/Screenshot%202024-05-22%20191732.png)   


9. **The default VPC and Subnet was used for the networking configuration.**   

![](./images/Screenshot%202024-05-22%20192314.png)   

   
### **Connect to Your Instance**
Open the terminal or SSH client.
Navigate into the directory where the .pem key was downloaded   
``` cd Downloads ```      

![](./images/Screenshot%202024-05-22%20231244.png)
    
Change permission for the private key file.   
    ``` chmod 0400 "private-key-name.pem"```

Connect to your instance using the key pair you selected:
``` ssh -i "private-key-name.pem" ubuntu@<Public-IP-address></Public-IP-address> ```      

![](./images/Screenshot%202024-05-22%20233612.png)

## **Step1. Installing Apache and Updating the Firewall**

**Apache: The web server software that serves as the middleman between the client's web browser and the web application. Apache is highly configurable and supports various features such as URL rewriting, virtual hosting, and authentication.**    
___  
   Install Apache using Ubuntu's package manager 'apt'  

1. Update the package index:   

   ``` sudo apt update```        

   ![](./images/Screenshot%202024-05-23%20002105.png) 

2. Upgrade the package index:   

   ``` sudo apt upgrade```      

   ![](./images/Screenshot%202024-05-23%20002248.png) 

3. Run Apache package installation:    

   ```sudo apt install apache2```     

   ![](./images/Screenshot%202024-05-23%20003445.png)   

4. Verify apache2 is running as a service in our OS by using the following command:   
   
   ```sudo systemctl status apache2```

   ![](./images/Screenshot%202024-05-23%20004418.png)


5. Open a web browser and try to access your Public IP address. In this case;
```http://http://16.171.197.144/:80```

![](./images/Screenshot%202024-05-23%20005536.png)


## **Step 2 - Installing MySQL**   
**MySQL: The relational database management system (RDBMS) used for storing and managing data in the web application. MySQL is known for its reliability, scalability, and performance, making it a popular choice for web developers.**   

1. **Acquire and install this software using:**
   
   ```sudo apt install mysql-server```

   ![](./images/Screenshot%202024-05-23%20011407.png)

2. **Enable and verify that mysql is running using the command:**

```sudo systemctl status mysql```     
  ![](./images/Screenshot%202024-05-23%20142718.png)

3. **When installation is finished, log in to the MySQL console by typing :**   
```sudo mysql```

   This connects to the MySQL server as the administrative database user root infered by the use of sudo when running the command.
   
![](./images/Screenshot%202024-05-23%20011456.png)
   
   4. **Set a password for root user using mysql_native_password as default authentication method.**    


   ```ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Admin.1```

   5. **Run an Interactive script to secure MySQL**

The security script comes pre-installed with mysql. This script removes some insecure settings and lock down access to the database system.

```sudo mysql_secure_installation```  
![](./images/Screenshot%202024-05-23%20143744.png)    

6. **After changing root user password, log in to MySQL console.**

A command prompt for password was noticed after running the command below.

```sudo mysql -p```

![](./images/Screenshot%202024-05-23%20144120.png)   

Exit MySQL shell

```exit```


## Step 3 - Install PHP   
1. Install php Apache is installed to serve the content and MySQL is installed to store and manage data. PHP is the component of the set up that processes code to display dynamic content to the end user.

The following were installed:

* php package  

* php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases.  

* libapache2-mod-php, to enable Apache to handle PHP files.
sudo apt install php libapache2-mod-php php-mysqls11  

```sudo apt install php libapache2-mod-php php-mysql```

![](./images/Screenshot%202024-05-23%20155820.png)

2. Confirm the PHP version

```php -v```
![](./images/Screenshot%202024-05-23%20154954.png)

At this point, the LAMP stack is completely installed and fully operational.
   
   ### To test the set up with a PHP script, it's best to set up a proper Apache Virtual Host to hold the website files and folders. Virtual host allows to have multiple websites located on a single machine and it won't be noticed by the website users.
___  


## **Step 4 - Create a virtual host for the website using Apache**
1. **The default directory serving the apache default page is /var/www/html. Create your document directory next to the default one.**

Created the directory for projectlamp using "mkdir" command

```sudo mkdir /var/www/projectlamp```   

Assign the directory ownership with $USER environment variable which references the current system user.

```sudo chown -R $USER:$USER /var/www/projectlamp1``` 

  
  Create and open a new configuration file in apache’s “sites-available” directory using vim.

```sudo vim /etc/apache2/sites-available/projectlamp.conf```  

![](./images/Screenshot%202024-05-23%20173134.png)


Past in the bare-bones configuration below by hitting on ```i```:    


`<VirtualHost *:80>
  ServerName projectlamp
  ServerAlias www.projectlamp
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/projectlamp
  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>`

hit the `esc` button on the keyboard, type `:` , type `wq.` for **w** and `q` for quit hit `ENTER`  to save the file.
  


 **Show the new file in sites-available**

```sudo ls /etc/apache2/sites-available```

![](./images/Screenshot%202024-05-23%20180558.png)    

With the VirtualHost configuration, Apache will serve projectlamp using /var/www/projectlamp1 as its web root directory.     

 **Enable the new virtual host**

```sudo a2ensite projectlamp1```  
![](./images/Screenshot%202024-05-23%20180633.png)

 **Disable apache’s default website.**

This is because Apache’s default configuration will overwrite the virtual host if not disabled. This is required if a custom domain is not being used.

```sudo a2dissite 000-default```
![](./images/Screenshot%202024-05-23%20180700.png)  

 **Ensure the configuration does not contain syntax error:**

```sudo apache2ctl configtest```

![](./images/Screenshot%202024-05-23%20181922.png)

Reload apache for changes to take effect.

```sudo systemctl reload apache2```

![]()    


 The new website is now active but the web root /var/www/projectlamp is still empty. Create an index.html file in this location so to test the virtual host work as expected.

```sudo echo 'Hello LAMP from David' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp1/index.html```  
 and then type  

```sudo systemctl reload apache2```

![](./images/Screenshot%202024-05-23%20185704.png)   

**Open the website on a browser using the public IP address.**

http://16.171.197.144/:80   

![](./images/Screenshot%202024-05-23%20190136.png)


  
  This file can be left in place as a temporary landing page for the application until an index.php file is set up to replace it. Once this is done, the index.html file should be renamed or removed from the document root as it will take precedence over index.php file by default.  
   

   ## **Step 5 - Enable PHP on the website**  

With the default DirectoryIndex setting on Apache, index.html file will always take precedence over index.php file. This is useful for setting up maintenance page in PHP applications, by creating a temporary index.html file containing an informative message for visitors. The index.html then becomes the landing page for the application. Once maintenance is over, the index.html is renamed or removed from the document root bringing back the regular application page. 
  
  If the behaviour needs to be changed, you'll need to edit the  `/etc/apache2/mods-enabled/dir.conf` and change the order in which the index.php file is listed within the DirectoryIndex directive:  
  1. Open the dir.conf file with vim to change the behaviour

```sudo vim /etc/apache2/mods-enabled/dir.conf```   

```
 <IfModule mod_dir.c>
  # Change this:
  # DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
  # To this:
  DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```  

![]()

Save and Exit vim

Press Esc to enter command mode.
Type `:wq` and press `Enter` to save the changes and exit vim.    

2. Reload Apache

Apache is reloaded so the changes takes effect.

```sudo systemctl reload apache2```

![](./images/Screenshot%202024-05-25%20233931.png)  


3. Create a php test script to confirm that Apache is able to handle and process requests for PHP files.  


A new index.php file was created inside the custom web root folder.

```vim /var/www/projectlamp1/index.php```  

![](./images/Screenshot%202024-05-25%20233527.png)

Add the text below in the index.php file

```
<?php
phpinfo()
```     
![](./images/Screenshot%202024-05-25%20225812.png)

4. Now refresh the page

![](./images/Screenshot%202024-05-25%20231029.png)

This page provides information about the server from the perspective of PHP. It is useful for debugging and to ensure the settings are being applied correctly.

After checking the relevant information about the server through this page, It’s best to remove the file created as it contains sensitive information about the PHP environment and the ubuntu server. It can always be recreated if the information is needed later.

```sudo rm /var/www/projectlamp1/index.php```   

### Conclusion:

The LAMP stack provides a robust and flexible platform for developing and deploying web applications. By following the guidelines outlined in this documentation, It was possible to set up, configure, and maintain a LAMP environment effectively, enabling the creation of powerful and scalable web solutions.


