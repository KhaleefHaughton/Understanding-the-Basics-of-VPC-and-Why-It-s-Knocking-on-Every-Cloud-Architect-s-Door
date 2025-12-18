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
4. [Setup Instructions](#setup-instructions)
5. [Step-by-Step Deployment](#step-by-step-deployment)
6. [Usage](#usage)
7. [File Structure](#file-structure)
8. [Troubleshooting](#troubleshooting)
9. [License](#license)
10. [Acknowledgements](#acknowledgements)

---

## Project Overview

The goal of this project is to deploy a **highly available and load-balanced web application** in AWS. The project accomplishes:

1. Creating a **VPC** with CIDR `10.10.0.0/16`
2. Creating **public subnets** across multiple Availability Zones
3. Launching EC2 instances with **user-data scripts** to install Apache and serve a web page
4. Configuring **security groups** for proper traffic control
5. Setting up an **ALB** to distribute traffic across EC2 instances
6. Using **Auto Scaling** to adjust the number of instances automatically based on demand

---

**Components:**

- **VPC** – isolates the network
- **Subnets** – public subnets in multiple Availability Zones
- **Internet Gateway (IGW)** – allows outbound internet access
- **Route Table** – routes traffic from subnets to IGW
- **Security Groups** – control inbound/outbound traffic
- **Launch Template** – defines EC2 instance configuration
- **Auto Scaling Group** – dynamically scales instances
- **Application Load Balancer** – distributes traffic to EC2 instances

---

## Prerequisites

Before deploying this project, you need:

1. **AWS CLI** installed and configured with credentials and region
2. **Python 3.8+** installed
3. **boto3** library installed:  
   ```bash
   pip install boto3
