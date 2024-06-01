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
