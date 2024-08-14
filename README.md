# AWS Deployment Guide for App1 and App2

### This guide details the process of deploying two lightweight web applications, "App1" and "App2," on AWS using EC2 instances and an Application Load Balancer (ALB) with path-based routing. Each application is deployed on two EC2 t2.micro instances for cost efficiency.

## Table of Contents
**Prerequisites**
Step 1: EC2 Instance Setup
Step 2: Security Group Configuration
Step 3: Application Load Balancer Setup with Path-Based Routing
Step 4: Testing and Validation
Nginx Configuration

### Prerequisites

An AWS account with access to the AWS Management Console.
SSH key pair for accessing EC2 instances.
Basic knowledge of AWS services (EC2, ALB, etc.).


## Step 1: EC2 Instance Setup

**Launch EC2 Instances**
Go to the EC2 Dashboard:

Navigate to the EC2 Dashboard in the AWS Management Console.

Launch Four EC2 Instances:

AMI: Amazon Linux 2 AMI.
Instance Type: t2.micro.
Network: Choose your VPC and subnets.
Security Groups: Select an existing security group or create a new one (we'll configure this in the next step).
Tags: Add tags for identification (e.g., "App1-Instance1," "App1-Instance2," "App2-Instance1," "App2-Instance2").
Key Pair: Select an existing key pair or create a new one for SSH access.
SSH into Each Instance:

Use the following command to SSH into each instance:

```
ssh -i your-key.pem ec2-user@<public-ip-address>
```

Deploy "App1" and "App2":

App1: Deploy "App1" on two instances.
App2: Deploy "App2" on the other two instances.
Use the following commands to set up a simple Nginx server (modify based on your application):


```
sudo yum update -y
sudo amazon-linux-extras install nginx1 -y
sudo systemctl start nginx
sudo systemctl enable nginx
```
Nginx Configuration:

## Step 2: Security Group Configuration

### Create Security Groups
Create a Security Group for EC2 Instances:

Inbound Rules:
HTTP (Port 80): Allow from anywhere.
SSH (Port 22): Allow only from your IP address.

Create a Security Group for ALB:

Inbound Rules:
HTTP (Port 80): Allow from anywhere.
Attach Security Groups:

Attach the appropriate security groups to the EC2 instances and the ALB.

## Step 3: Application Load Balancer Setup with Path-Based Routing

### Create an Application Load Balancer (ALB)

Go to the EC2 Dashboard:
Navigate to the Load Balancers section in the EC2 Dashboard.
Create an ALB:
Name: Provide a name for the ALB.
Scheme: Internet-facing.
Listeners: Add a listener on port 80.
Availability Zones: Select the VPC and subnets where your EC2 instances are running.
Configure Target Groups
Create Two Target Groups:

Target Group 1:
Name: app1-target-group.
Target Type: Instance.
Protocol: HTTP.
Port: 80.
Health Check Path: /app1.
Target Group 2:
Name: app2-target-group.
Target Type: Instance.
Protocol: HTTP.
Port: 80.
Health Check Path: /app2.
Register EC2 Instances:

Register the "App1" instances with app1-target-group.
Register the "App2" instances with app2-target-group.
Configure Path-Based Routing
Set Up Routing Rules:

In the ALB listener settings, add rules for path-based routing:
/app1: Forward to app1-target-group.
/app2: Forward to app2-target-group.
Review and Create the ALB:

Review your settings and create the ALB.

## Step 4: Testing and Validation

### Test Path-Based Routing
Access the ALB DNS Name:
Open a browser and navigate to the ALB's DNS name:
http://<ALB-DNS-Name>/app1: This should route to the "App1" instances.
http://<ALB-DNS-Name>/app2: This should route to the "App2" instances.
Security Validation
SSH Access:
Attempt to SSH into the EC2 instances using their public IPs to confirm that only your IP address can access them.	

Nginx Configuration
For each application, replace the default Nginx configuration with the following:

Configuration for "App1" (/etc/nginx/nginx.conf):

download the nginx.conf file from repo.


## Output:

![image](https://github.com/user-attachments/assets/11b2592f-3cf1-4709-8313-47e5993781a1)
![image](https://github.com/user-attachments/assets/e0d272f1-a0a9-472a-84f8-6152ae5e95fc)
![image](https://github.com/user-attachments/assets/196d49ab-d698-4a48-b9af-c487c5fd2efd)
![image](https://github.com/user-attachments/assets/e9ac2479-532f-4bf9-8879-81460b71c25f)
![image](https://github.com/user-attachments/assets/d3a76a55-8ea4-44ab-8b93-262154e01066)
![image](https://github.com/user-attachments/assets/8b3ab4b1-96a4-4bb2-97fb-425d6c3b2188)
![image](https://github.com/user-attachments/assets/15da59fa-8528-4aaa-ae42-d37e510615dd)
![image](https://github.com/user-attachments/assets/d26c0cc2-4f1a-4286-901f-adee68cdeda7)

![image](https://github.com/user-attachments/assets/8d9a2b3c-d3a4-4ec9-80a8-12be121d6537)
![image](https://github.com/user-attachments/assets/3c8a7d73-10ec-45ec-b243-6f91f4496d49)
![image](https://github.com/user-attachments/assets/d882796b-4565-406c-bddd-e03f08d9804b)
![image](https://github.com/user-attachments/assets/8d589b56-4f9f-4a93-a7ce-643680a9d1c8)
![image](https://github.com/user-attachments/assets/4db29042-bfbd-49d3-8085-2bc482038143)
![image](https://github.com/user-attachments/assets/da624b40-141d-4f89-9004-e5358c57bff1)
![image](https://github.com/user-attachments/assets/2c393563-f0b9-419a-bc14-05d50f643a9a)
![image](https://github.com/user-attachments/assets/e5b1c00b-7201-4bce-aec4-a156e818c456)
![image](https://github.com/user-attachments/assets/78c1486c-9945-4198-8ee0-5fbcfbe5ff96)
![image](https://github.com/user-attachments/assets/049d27fe-fa02-43e1-bcd9-21515dabce96)

![image](https://github.com/user-attachments/assets/8fb013c4-5b54-4f52-969f-69defcbc4c7a)
![Screenshot from 2024-08-14 22-42-09](https://github.com/user-attachments/assets/bbeeef0b-45ce-4aaf-8fed-e9d2d989cfad)
![image](https://github.com/user-attachments/assets/297d4fbb-1468-4e11-8a12-065e718ce560)
















