# **WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS**

**Introduction: <br/>
This guide provides a step-by-step approach to deploying a LAMP stack (Linux, Apache, MySQL, PHP) on AWS. The LAMP stack is a popular open-source web platform used to run dynamic websites and servers.** <br/> 

## **Step 0 - Preparing Prerequisites:** <br/>
For this project, an AWS account and a virtual server with Ubuntu Server OS is needed


### Launch an EC2 Instance  
1. Log in to the AWS Management Console.<br/>
![Login page](./images/Screenshot%202024-05-22%20171732.png)

![](./images/Screenshot%202024-05-22%20180009.png)

2. Navigate to the EC2 Dashboard and click on "Launch Instance".
![](./images/Screenshot%202024-05-22%20180548.png)


3. Choose an Amazon Machine Image (AMI):

i. Select an AMI that is based on Linux (e.g. Ubuntu Server).
![](./images/Screenshot%202024-05-22%20182017.png)

4. Choose an Instance Type:
 Select an instance type (e.g., t3.micro, which is eligible for the free tier).   
![](./images/Screenshot%202024-05-22%20182725.png)

5. Configure key pair login:
create a new key pair.
![](./images/Screenshot%202024-05-22%20183805.png)

6. Configure the number of instances, network, as required.
![](./images/Screenshot%202024-05-22%20185906.png)


7. Specify the storage size (default is typically sufficient for testing).
![](./images/Screenshot%202024-05-22%20185906.png)

8. Set inbound rules:
- Allow traffic on port 80 (HTTP) with source from anywhere on the internet.
- Allow traffic on port 443 (HTTPS) with source from anywhere on the internet.
- Allow traffic on port 22 (SSH) with source from any IP address. This is opened by default.
![](./images/Screenshot%202024-05-22%20191732.png)

9. The default VPC and Subnet was used for the networking configuration.
![](./images/Screenshot%202024-05-22%20192314.png)