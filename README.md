# Understanding-the-Basics-of-VPC-and-Why-Its-Knocking-on-Every-Cloud-Architects-Door
Ping Ping, Who’s There? It’s Your VPC Asking for Attention!

# AWS VPC with Auto Scaling & Load Balancer

This repository automates the creation of a **scalable web application environment** on AWS, including:

- Custom **VPC** with public subnets
- **Auto Scaling Group (ASG)** of EC2 instances running Apache
- **Application Load Balancer (ALB)**
- Security groups configured to allow only ALB-to-EC2 traffic

The setup follows the Medium article ["Ping Ping, Who’s There? It’s Your VPC Asking for Attention!"](https://medium.com/@KhaleefHaughton/ping-ping-whos-there-it-s-your-vpc-asking-for-attention-193231974330).

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Architecture](#architecture)
3. [Prerequisites](#prerequisites)
4. [Step-by-Step Deployment](#step-by-step-deployment)

---

## 1. Project Overview

The goal of this project is to deploy a **highly available and load-balanced web application** in AWS. The project accomplishes:

1. Creating a **VPC** with CIDR `10.10.0.0/16`
2. Creating **public subnets** across multiple Availability Zones
3. Launching EC2 instances with **user-data scripts** to install Apache and serve a web page
4. Configuring **security groups** for proper traffic control
5. Setting up an **ALB** to distribute traffic across EC2 instances
6. Using **Auto Scaling** to adjust the number of instances automatically based on demand

---

## 2. Architecture Components

- **VPC** – isolates the network
- **Subnets** – public subnets in multiple Availability Zones
- **Internet Gateway (IGW)** – allows outbound internet access
- **Route Table** – routes traffic from subnets to IGW
- **Security Groups** – control inbound/outbound traffic
- **Launch Template** – defines EC2 instance configuration
- **Auto Scaling Group** – dynamically scales instances
- **Application Load Balancer** – distributes traffic to EC2 instances

---

## 3. Prerequisites

Before deploying this project, you need:

1. **AWS CLI** installed and configured with credentials and region
2. **Python 3.8+** installed
3. **boto3** library installed:  
   ```bash
   pip install boto3


Step-by-Step Deployment



## Step 1: Create the VPC (CDA02_Project_VPC)

Uses the CIDR 10.10.0.0/16

Enables DNS support and hostnames


## Step 2: Create Public Subnets

Creates 3 subnets, each in a different Availability Zones (CDA02_Project_FirstSubnet), (CDA02_Project_SecondSubnet),(CDA02_Project_ThirdSubnet)


Enables automatic public IP assignment


## Step 3: Create an Internet Gateway (CDA02_IGW_Project)

Attached the IGW to the VPC

Provides internet access for public subnets


## Step 4: Configure Route Table (rtb-09adfe4212e743774)

Creates a route table for the VPC 

Adds a default route to the Internet Gateway

Associates route table with public subnets


## Step 5: Create Security Groups

WebServerSG: allows HTTP from ALB only

LoadBalancerSG: allows HTTP from anywhere


## Step 6: Launch Template (CDA02_Launch_Temp)

Defines the EC2 instance configuration

Includes user-data script for Apache setup

```
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo “<h1> WELCOME TO MY PURE IMAGINATION (private IP address) $(hostname -f)</h1>” > /var/www/html/index.html

```

## Step 7: Create Auto Scaling Group (CDA02_Project_ASG)

Launches EC2 instances from the Launch Template

Sets min and max instance counts

Associates instances with the public subnets


## Step 8: Create Application Load Balancer

Internet-facing ALB distributes traffic to EC2 instances

Added Target group to Load Balancer (CDA02ProjectTGN)

Outputs the DNS name of the ALB for access

