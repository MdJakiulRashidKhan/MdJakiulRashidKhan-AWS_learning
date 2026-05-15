## 📌 Project Repository Name

aws-vpc-alb-auto-scaling-project


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

## 📈 Auto Scaling Test & Dynamic Scaling Policy

After creating the Auto Scaling Group, I verified that the desired capacity was working correctly.

---

## 🖥️ Instance Behavior Check

- Initially, the **desired capacity was set to 3**
- So, **3 EC2 instances were automatically launched**
- When accessing the Load Balancer DNS in the browser, it displayed responses from all 3 instances (hostname rotation confirmed)

---

## 🧪 Manual Instance Termination Test

To test Auto Scaling behavior:

- I manually terminated 1 EC2 instance
- AWS Auto Scaling detected the instance failure
- It automatically launched a new instance to maintain the desired capacity of 3

👉 This confirmed that Auto Scaling is working correctly

---

## ⚙️ Dynamic Scaling Policy (Target Tracking)

I configured a **Target Tracking Scaling Policy**:

- **Policy Type:** Target Tracking Scaling  
- **Metric Type:** Average CPU Utilization  
- **Target Value:** 50%  
- **Instance Warm-up Time:** 300 seconds  

---

## 📌 What This Policy Does

This policy automatically adjusts the number of EC2 instances based on CPU usage:

- If CPU usage increases above 50% → new instances are launched (Scale Out)
- If CPU usage drops below 50% → instances are removed (Scale In)

👉 This ensures performance stability and cost efficiency

---

## 🔥 Load Testing (Stress Test)

To simulate high CPU usage:

### On each EC2 instance:

- Installed stress tool:
  sudo yum install stress -y
- Applied CPU load:
  stress --cpu 2 --timeout 600

  ## 🧠 What Happened During Load Test

- CPU usage increased significantly on the running instances due to simulated workload
- The Target Tracking Scaling Policy continuously monitored the CPU utilization
- When CPU usage went above the defined threshold, Auto Scaling automatically triggered scale-out actions
- New EC2 instances were launched to handle the increased load

---

## 📈 Scaling Result

- The number of instances increased from **3 to 6**
- Load was distributed across all running instances through the Load Balancer
- The system maintained stability and high availability even under heavy traffic
  
  ---
## 🖼️ Screenshots

![](img/39.png)
![](img/40.png)
![](img/41.png)
![](img/42.png)
![](img/43.png)
![](img/44.png)
![](img/45.png)
![](img/46.png)
![](img/47.png)

![](img/b1.png)
![](img/b2.png)
![](img/b3.png)

![](img/48.png)

---

## 🚀 Project Summary

This project demonstrates a complete AWS Auto Scaling architecture using a custom VPC, Application Load Balancer (ALB), Target Group, and Auto Scaling Group (ASG).

A secure VPC was created with both public and private subnets across multiple Availability Zones to ensure high availability and fault tolerance. An Internet Gateway and route tables were configured to enable controlled internet access.

An Application Load Balancer was deployed to distribute incoming traffic across multiple EC2 instances. A Target Group was created and associated with the Load Balancer to monitor healthy instances.

An Auto Scaling Group was then configured using a Launch Template with Amazon Linux EC2 instances running Nginx as a web server. The instances were automatically deployed across multiple subnets and registered with the Target Group.

To ensure dynamic scalability, a Target Tracking Scaling Policy was implemented based on average CPU utilization (50%). Under normal conditions, 3 instances were running, but during increased load testing, the system automatically scaled out to 6 instances.

A stress test was performed to simulate high CPU usage, which triggered Auto Scaling actions. The system successfully demonstrated both scale-out and self-healing capabilities by replacing terminated instances and distributing traffic evenly through the Load Balancer.

Overall, this project successfully implements a highly available, scalable, and fault-tolerant AWS architecture suitable for real-world production environments.

---



 

