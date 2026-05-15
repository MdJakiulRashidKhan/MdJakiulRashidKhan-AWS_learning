# ☁️ AWS VPC Setup for Auto Scaling

## 🎯 Project Overview
In this project, I created an AWS VPC for an Auto Scaling architecture. It includes both public and private subnets to ensure a secure and scalable network design.

---

## ⚙️ VPC Configuration

- **VPC Name:** autoscalling-vpc  
- **IPv4 CIDR Block:** 10.0.0.0/16  
- **Tenancy:** Default  

---

## 🌐 Subnet Configuration

### 📌 Public Subnets (3)
- Public Subnet 1  
- Public Subnet 2  
- Public Subnet 3  

👉 These subnets are created across 3 different Availability Zones (AZs).

---

### 🔒 Private Subnets (3)
- Private Subnet 1  
- Private Subnet 2  
- Private Subnet 3  

---

## 🛣️ Network Components

### Internet Gateway (IGW)
- One Internet Gateway is created and attached to the VPC.

---

## 📊 Route Tables

### 🌍 Public Route Table
- One Route Table is created for Public Subnets  
- It is associated with the Internet Gateway  

### 🔐 Private Route Table
- One Route Table is created for Private Subnets  
- NAT Gateway is not used (NAT: None)

---

## 🧩 Additional Settings

- NAT Gateway: ❌ None  
- VPC Endpoint: ❌ None  
- Availability Zones: 3 AZs  

---

## 🖼️ Architecture Screenshots


![VPC Overview](img/1.png)


![Subnets](img/2.png)


![Route Tables](img/3.png)


![Architecture](img/4.png)

---

## 🧩 Target Group Setup (EC2 Dashboard)

I navigated to the EC2 Dashboard and created a Target Group for the Auto Scaling + Load Balancer setup.

---

## ⚙️ Target Group Configuration

- **Target Type:** Instance  
- **Name:** asg-alb-tg  
- **Protocol:** HTTP  
- **Port:** 80  
- **IP Address Type:** IPv4  
- **VPC:** autoscalling-vpc  

---

## 🧪 Health Check Configuration

- **Health Check Protocol:** HTTP  
- **Health Check Path:** /  

---

## 🚨 Important Note

At this stage, no instances were available, so no targets were registered.

Also:
- Load Balancer: ❌ None associated

---

## 🖼️ Screenshots

![](img/5.png)

![](img/6.png)

![](img/7.png)

![](img/8.png)

![](img/9.png)

![](img/10.png)

![](img/11.png)

![](img/12.png)

---

## ⚖️ Application Load Balancer (ALB) Setup

I navigated to the EC2 Dashboard and created an Application Load Balancer for the Auto Scaling architecture.

---

## ⚙️ Load Balancer Configuration

- **Load Balancer Type:** Application Load Balancer  
- **Name:** asg-alb  
- **Scheme:** Internet-facing  
- **IP Address Type:** IPv4  

---

## 🌐 Network Mapping

- **VPC:** autoscalling-vpc  
- **Availability Zones:** 3 public subnets selected  

---

## 🔐 Security Group Configuration

A new Security Group was created:

- **Security Group Name:** asg-sg  
- **Description:** Allow HTTP requests for Auto Scaling VPC  
- **VPC:** autoscalling-vpc  

### 📥 Inbound Rules
- **Type:** HTTP  
- **Port:** 80  
- **Source:** 0.0.0.0/0  

---

## 🎯 Listener & Routing

- **Protocol:** HTTP  
- **Port:** 80  
- **Target Group:** asg-alb-tg  

---

## 🚀 Final Step

After reviewing all configurations, the Load Balancer was created successfully.

---

## 🖼️ Screenshots

![](img/13.png)

![](img/14.png)

![](img/15.png)

![](img/16.png)

![](img/17.png)

![](img/18.png)

![](img/19.png)

![](img/20.png)

---

## 🚀 Auto Scaling Group Setup (EC2 Dashboard)

I navigated to the EC2 Dashboard and created an Auto Scaling Group for the Application Load Balancer architecture.

---

## ⚙️ Auto Scaling Group Configuration

- **Name:** asg-ec2-group  

---

## 🧱 Launch Template Creation

I created a Launch Template with the following configuration:

- **Name:** asg-launch-template  
- **Description:** Launch template for Auto Scaling EC2 instances behind ALB  
- **AMI (OS Image):** Amazon Linux  
- **Instance Type:** t3.micro  
- **Key Pair:** asg-key  
- **Subnet:** Not included in Launch Template  

---

## 🔐 Security Group for Launch Template

A new Security Group was created:

- **Name:** lt-sg  
- **Description:** Allow SSH and HTTP access  
- **VPC:** autoscaling-vpc  

### 📥 Inbound Rules
- SSH (22) → 0.0.0.0/0  
- HTTP (80) → 0.0.0.0/0  

---

## ⚙️ Launch Template Network Settings

- **Security Group:** lt-sg (selected existing)  
- **Auto-assign Public IP:** Enabled  

---

## 🖥️ User Data Script Explanation

A startup script was added in **Advanced Details → User Data**.

### 📌 What this script does:

- Updates the system packages
- Installs Nginx web server
- Starts and enables Nginx service
- Creates a custom HTML page
- Displays instance hostname and IP address dynamically
- Restarts Nginx to apply changes

### 🔧 Main Purpose:

👉 This script automatically configures each EC2 instance as a web server when it launches  
👉 It helps demonstrate that Auto Scaling is working properly behind the Load Balancer  

---

## 🌐 Auto Scaling Group Configuration Steps

After creating the Launch Template:

### 📍 Network Settings
- **VPC:** autoscaling-vpc  
- **Availability Zones & Subnets:** Selected 3 subnets  

---

### ⚖️ Load Balancer Integration

- **Attach to existing load balancer:** Selected  
- **Target Group:** asg-alb-tg  

---

### ❤️ Health Check Configuration

- **Health Check Type:** Elastic Load Balancer  
- **Health Check Period:** 20 seconds  

---

## 📊 Scaling Configuration

- **Desired Capacity:** 3  
- **Minimum Capacity:** 1  
- **Maximum Capacity:** 6  

---

## 🔔 Additional Settings

- Notifications: Not configured  
- Tags: Not configured  

---

## 🚀 Final Step

After reviewing all configurations, the Auto Scaling Group was successfully created.

---

## 🖼️ Screenshots

![](img/21.png)
![](img/22.png)
![](img/23.png)
![](img/24.png)
![](img/25.png)
![](img/26.png)
![](img/27.png)
![](img/28.png)
![](img/29.png)
![](img/30.png)
![](img/31.png)
![](img/32.png)
![](img/33.png)
![](img/34.png)
![](img/35.png)
![](img/36.png)
![](img/37.png)
![](img/38.png)

---   

