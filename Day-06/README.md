# 📦 Amazon VPC Setup for EBS Project

## 📌 Overview
This project demonstrates the creation of a simple AWS VPC setup for working with EC2 and EBS resources.

---

## 🏗️ Step 1: Create VPC

First, I went to the AWS VPC Dashboard and selected **Create VPC**.

Then I used the **VPC and More** option and configured the following settings:

---

## ⚙️ VPC Configuration

- **VPC Name:** jakiul-ebs-vpc  
- **IPv4 CIDR Block:** 10.0.0.0/16  
- **Tenancy:** Default  

---

## 🌐 Subnet Configuration

- **Availability Zone:** 1  
- **Public Subnet:** 1  
- **Private Subnet:** 0  

---

## 🔗 Networking Setup

- **NAT Gateway:** None  
- **VPC Endpoint:** None  

---

## 🚀 Resources Created Automatically

After creating the VPC, AWS automatically created:

- 1 VPC  
- 1 Public Subnet  
- Internet Gateway (IGW) attached  
- Route Table configured for public access  

---

## 🖼️ Screenshots

![img1](./images/img1.png)  
![img2](./images/img2.png)  
![img3](./images/img3.png)  
![img4](./images/img4.png)
