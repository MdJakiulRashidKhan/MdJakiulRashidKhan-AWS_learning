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

## 🚀 Summary
This VPC setup provides a basic foundation for an Auto Scaling architecture, where public and private subnets are properly separated for security and scalability.
