# 🌐 AWS NAT Gateway Setup Guide

## Step 0: Select Region

AWS Console-এ গিয়ে Ohio State region select করেছি।  
![Ohio Region Screenshot](img/0.png)

## Step 1: Create VPC

VPC Dashboard-এ গিয়ে **Create VPC** এ গিয়েছি।  
- **VPC Name:** test-vpc  
- **IPv4 CIDR block:** 10.0.0.0/16  
- **IPv6 CIDR block:** None  
- **Tenancy:** Default  
- **VPC Encryption:** None  

✅ Create VPC সফলভাবে সম্পন্ন হয়েছে।  
![Create VPC Screenshot](img/1.png)
![Create VPC Screenshot](img/1.png)

## Step 1.1: Create Subnets

VPC Dashboard-এ গিয়ে **Subnets** এ গিয়েছি।  
**Create Subnet** এ click করেছি।  
![Create Subnets Screenshot](img/3.png)
![Create Subnets Screenshot](img/4.png)

### Public Subnet
- **VPC ID:** test-vpc  
- **Subnet Name:** test-pub-subnet-01  
- **Availability Zone:** us-east-2a  
- **IPv4 CIDR block:** 10.0.1.0/24
 ✅ Subnets সফলভাবে create হয়েছে। 
  ![Create Subnets Screenshot](img/5.png)

### Private Subnet
- **VPC ID:** test-vpc  
- **Subnet Name:** test-pvt-subnet-01  
- **Availability Zone:** us-east-2a  
- **IPv4 CIDR block:** 10.0.2.0/24  

✅ Subnets সফলভাবে create হয়েছে।  
![Create Subnets Screenshot](img/6.png)

## Step 1.2: Create and Attach Internet Gateway

VPC Dashboard-এ গিয়ে **Internet Gateways** এ গিয়েছি। 
![Create & Attach IGW Screenshot](img/7.png)
**Create Internet Gateway** এ click করেছি। 
![Create & Attach IGW Screenshot](img/8.png)

- **Internet Gateway Name:** test-igw  
- Click **Create Internet Gateway**।  
- Internet Gateway সফলভাবে create হয়েছে।
  ![Create & Attach IGW Screenshot](img/9.png)

এরপর **VPC Attach** করেছি:  
- **VPC:** test-vpc
  

✅ Internet Gateway test-vpc তে attach হয়েছে।  
![Create & Attach IGW Screenshot](img/10.png)
![Create & Attach IGW Screenshot](img/11.png)

## Step 1.3: Create Route Tables for Public & Private Subnets

### Public Route Table
VPC Dashboard-এ গিয়ে **Route Tables** এ গিয়েছি।  
**Create Route Table** এ click করেছি।  
![Private Route Table Screenshot](img/12.png)
![Private Route Table Screenshot](img/13.png)

- **Route Table Name:** test-pub-rt  
- **VPC:** test-vpc  
- Click **Create Route Table** ✅
- ![Private Route Table Screenshot](img/9.png)

**Configure Routes:**  
- **Edit Routes** → **Add Route:** Destination `0.0.0.0/0` → Target: **Internet Gateway (test-igw)**
  ![Private Route Table Screenshot](img/15.png)
  ![Private Route Table Screenshot](img/16.png)
  ![Private Route Table Screenshot](img/17.png)
- Save routes ✅  

**Associate Subnet:**  
- **Edit Subnet Associations** → **Select Subnet:** test-pub-subnet-01
- ![Private Route Table Screenshot](img/18.png)
- ![Private Route Table Screenshot](img/19.png)
- Save associations ✅  


---

### Private Route Table
**Create Route Table** এ click করেছি।  

- **Route Table Name:** test-pvt-rt  
- **VPC:** test-vpc  
- Click **Create Route Table** ✅
  ![Private Route Table Screenshot](img/20.png)

**Associate Subnet:**  
- **Edit Subnet Associations** → **Select Subnet:** test-pvt-subnet-01  
- Save associations ✅
- ![Private Route Table Screenshot](img/21.png)
- ![Private Route Table Screenshot](img/22.png)

## Step 1.4: Create NAT Gateway and Update Private Route Table

VPC Dashboard-এ গিয়ে **NAT Gateways** এ গিয়েছি।  
**Create NAT Gateway** এ click করেছি।  
![Private Route Table with NAT Gateway Screenshot](img/23.png)

- **NAT Gateway Name:** test-natgw  
- **Region / VPC:** test-vpc  
- **Connectivity:** Public  
- **Elastic IP Allocation Method:** Automatic  

Click **Create NAT Gateway** ✅  
![Create NAT Gateway Screenshot](img/24.png)

---

### Update Private Route Table
- **Route Tables** এ গিয়ে **test-pvt-rt** select করেছি।  
- **Edit Routes** → **Add Route**:  
  - **Destination:** 0.0.0.0/0  
  - **Target:** NAT Gateway (test-natgw)  
- Save routes ✅  
![Private Route Table with NAT Gateway Screenshot](img/25.png)
![Private Route Table with NAT Gateway Screenshot](img/26.png)
![Private Route Table with NAT Gateway Screenshot](img/27.png)

## Step 2: Launch EC2 Instance

EC2 Dashboard-এ গিয়ে **Launch Instance** করেছি।  
![Launch EC2 Instance Screenshot](img/29.png)

## Step 2.1: Launch EC2 in Public Subnet

- **Instance Name:** test-pub-ec2  
- **AMI:** Amazon Linux  
- **Instance Type:** t2.micro  
- **Key Pair:** test-nat-key  
- **Network / Subnet:** test-pub-subnet-01  
- **Auto-assign Public IP:** Enable  

### Security Group
- **SSH (TCP 22):** 0.0.0.0/0  
- **HTTP (TCP 80):** 0.0.0.0/0  

Baki sob default রেখে **Launch Instance** ✅  

![Launch Public EC2 Screenshot](img/30.png)
![Launch Public EC2 Screenshot](img/31.png)
![Launch Public EC2 Screenshot](img/32.png)
![Launch Public EC2 Screenshot](img/33.png)

## Step 2.2: Launch EC2 in Private Subnet

- **Instance Name:** test-pvt-ec2  
- **AMI:** Amazon Linux  
- **Instance Type:** t2.micro  
- **Network / Subnet:** test-pvt-subnet-01  

### Security Group
- **SSH (TCP 22):** Anywhere (0.0.0.0/0)  
- **All Traffic:** Custom, Source 10.0.0.0/16  

✅ EC2 instance private subnet-এ সফলভাবে launch হয়েছে।  
![Launch Private EC2 Screenshot](img/34.png)
![Launch Private EC2 Screenshot](img/35.png)

## Step 3: Connect to Public EC2 via SSH

- **Connect to Public EC2:** SSH client ব্যবহার করেছি।  
- **Downloads Folder** এ গিয়েছি, **test-nat-key.pem** save আছে।  
- **Set Permissions:**  
```bash
chmod 400 test-nat-key.pem
ssh -i "test-nat-key.pem" ec2-user@<Public-EC2-IP>
```
![Launch Private EC2 Screenshot](img/36.png)
![Launch Private EC2 Screenshot](img/t1.png)

## Step 3.1: Verify Internet Access from Public EC2

- Public EC2 server-এ login হয়ে **internet connectivity** check করতে ping command চালিয়েছি:  
```bash
ping -c 4 google.com
```
![Launch Private EC2 Screenshot](img/t2.png)

## Step 3.2: Save Key on Server (Why We Did This)

- আমরা **private EC2 instance**-এ connect করতে চাই।  
- Private EC2-তে সরাসরি internet নেই, তাই **public EC2** (bastion/jump host) ব্যবহার করি।  
- এজন্য **PEM key** public EC2-তে copy করে save করেছি।  
- পরে এই key দিয়ে **SSH agent বা direct SSH** ব্যবহার করে private EC2-তে connect করা যাবে।  

✅ Key file public server-এ save করার মাধ্যমে private subnet EC2-তে secure access নিশ্চিত হলো।  
![Save Key on Server Screenshot](img/t3.png)

## Step 4: Connect to Private EC2 via Public EC2 (Bastion)

- **SSH Client** ব্যবহার করে **private EC2**-তে connect করেছি।  
- **Set Permissions:**  
```bash
chmod 400 test-nat-key.pem
ssh -i "test-nat-key.pem" ec2-user@<Private-EC2-Private-IP>
```
![Save Key on Server Screenshot](img/37.png)
![Save Key on Server Screenshot](img/t4.png)

## Step 4.1: Verify Internet Access from Private EC2

- Private EC2 server-এ login হয়ে **internet connectivity** check করতে ping command চালিয়েছি:  
```bash
ping -c 4 google.com
```
![Save Key on Server Screenshot](img/t5.png)










