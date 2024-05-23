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
MySQL: The relational database management system (RDBMS) used for storing and managing data in the web application. MySQL is known for its reliability, scalability, and performance, making it a popular choice for web developers.   
1. Acquire and install this software using:
   
   ```sudo apt install mysql-server```

   ![](./images/Screenshot%202024-05-23%20011407.png)


2. When installation is finished, log in to the MySQL console by typing :   
```sudo mysql```
![](./images/Screenshot%202024-05-23%20011456.png)
