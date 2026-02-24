# 🌐 Complete AWS NAT Gateway Setup with Public & Private EC2 Instances(day 3) 🚀

A step-by-step guide to creating a VPC, subnets, NAT Gateway, and launching EC2 instances in both public and private subnets on AWS.

---

## 📑 Table of Contents

1. [Step 0: Select Region 🌍](#step-0-select-region-🌍)  
2. [Step 1: Create VPC 🏗️](#step-1-create-vpc-🏗️)  
3. [Step 1.1: Create Subnets 🗂️](#step-11-create-subnets-🗂️)  
4. [Step 1.2: Create and Attach Internet Gateway 🌐](#step-12-create-and-attach-internet-gateway-🌐)  
5. [Step 1.3: Create Route Tables for Public & Private Subnets 🛣️](#step-13-create-route-tables-for-public--private-subnets-🛣️)  
6. [Step 1.4: Create NAT Gateway and Update Private Route Table 🛡️](#step-14-create-nat-gateway-and-update-private-route-table-🛡️)  
7. [Step 2: Launch EC2 Instances 💻](#step-2-launch-ec2-instances-💻)  
   - [2.1: Launch EC2 in Public Subnet](#21-launch-ec2-in-public-subnet)  
   - [2.2: Launch EC2 in Private Subnet](#22-launch-ec2-in-private-subnet)  
8. [Step 3: Connect to Public EC2 via SSH 🔑](#step-3-connect-to-public-ec2-via-ssh-🔑)  
   - [3.1: Verify Internet Access from Public EC2 🌐](#31-verify-internet-access-from-public-ec2-🌐)  
   - [3.2: Save Key on Server (Why We Did This) 🔐](#32-save-key-on-server-why-we-did-this-🔐)  
9. [Step 4: Connect to Private EC2 via Public EC2 (Bastion) 🏰](#step-4-connect-to-private-ec2-via-public-ec2-bastion-🏰)  
   - [4.1: Verify Internet Access from Private EC2 🌐](#41-verify-internet-access-from-private-ec2-🌐)  

## Step 0: Select Region 🌍

Logged into the AWS Console and selected the **Ohio (US-East) region**.  
This region will be used to deploy our VPC, subnets, and EC2 instances.

✅ Region successfully selected.  
![Ohio Region Screenshot](img/0.png)

## Step 1: Create VPC 🏗️

Navigated to the **VPC Dashboard** and clicked **Create VPC**.  

- **VPC Name:** test-vpc  
- **IPv4 CIDR block:** 10.0.0.0/16  
- **IPv6 CIDR block:** None  
- **Tenancy:** Default  
- **VPC Encryption:** None  

✅ VPC successfully created.  
![Create VPC Screenshot](img/1.png)
![Create VPC Screenshot](img/2.png)

## Step 1.1: Create Subnets 🗂️

Navigated to the **Subnets** section in the VPC Dashboard and clicked **Create Subnet**.  
![Create Subnets Screenshot](img/3.png)
![Create Subnets Screenshot](img/4.png)

### Public Subnet 🌐
- **VPC ID:** test-vpc  
- **Subnet Name:** test-pub-subnet-01  
- **Availability Zone:** us-east-2a  
- **IPv4 CIDR block:** 10.0.1.0/24  

✅ Public subnet successfully created.  
![Public Subnet Screenshot](img/5.png)

### Private Subnet 🔒
- **VPC ID:** test-vpc  
- **Subnet Name:** test-pvt-subnet-01  
- **Availability Zone:** us-east-2a  
- **IPv4 CIDR block:** 10.0.2.0/24  

✅ Private subnet successfully created.  
![Private Subnet Screenshot](img/6.png)

## Step 1.2: Create and Attach Internet Gateway 🌐

Navigated to the **Internet Gateways** section in the VPC Dashboard and clicked **Create Internet Gateway**.  
![Internet Gateways Dashboard](img/7.png)
![Click Create Internet Gateway](img/8.png)

- **Internet Gateway Name:** test-igw  
- Click **Create Internet Gateway**  

✅ Internet Gateway successfully created.  
![Internet Gateway Created Screenshot](img/9.png)

Next, attached the Internet Gateway to our VPC:  
- **VPC:** test-vpc  

✅ Internet Gateway successfully attached to **test-vpc**.  
![VPC Attached Screenshot 1](img/10.png)
![VPC Attached Screenshot 2](img/11.png)

## Step 1.3: Create Route Tables for Public & Private Subnets 🛣️

### Public Route Table 🌐
Navigated to the **Route Tables** section in the VPC Dashboard and clicked **Create Route Table**.  
![Route Tables Dashboard](img/12.png)
![Click Create Route Table](img/13.png)

- **Route Table Name:** test-pub-rt  
- **VPC:** test-vpc  
- Click **Create Route Table** ✅  
![Public Route Table Created](img/14.png)

**Configure Routes:**  
- Go to **Edit Routes** → **Add Route**  
  - **Destination:** 0.0.0.0/0  
  - **Target:** Internet Gateway (test-igw)  
- Save routes ✅  
![Edit Routes 1](img/15.png)
![Edit Routes 2](img/16.png)
![Edit Routes 3](img/17.png)

**Associate Subnet:**  
- **Edit Subnet Associations** → Select **test-pub-subnet-01** → Save ✅  
![Associate Public Subnet 1](img/18.png)
![Associate Public Subnet 2](img/19.png)

---

### Private Route Table 🔒
Click **Create Route Table** again.  

- **Route Table Name:** test-pvt-rt  
- **VPC:** test-vpc  
- Click **Create Route Table** ✅  
![Private Route Table Created](img/20.png)

**Associate Subnet:**  
- **Edit Subnet Associations** → Select **test-pvt-subnet-01** → Save ✅  
![Associate Private Subnet 1](img/21.png)
![Associate Private Subnet 2](img/22.png)

## Step 1.4: Create NAT Gateway and Update Private Route Table 🛡️

Navigated to the **NAT Gateways** section in the VPC Dashboard and clicked **Create NAT Gateway**.  
![NAT Gateways Dashboard](img/23.png)

- **NAT Gateway Name:** test-natgw  
- **Region / VPC:** test-vpc  
- **Connectivity:** Public  
- **Elastic IP Allocation Method:** Automatic  

Click **Create NAT Gateway** ✅  
![NAT Gateway Created](img/24.png)

---

### Update Private Route Table 🔒
- Go to **Route Tables** and select **test-pvt-rt**  
- **Edit Routes** → **Add Route**  
  - **Destination:** 0.0.0.0/0  
  - **Target:** NAT Gateway (test-natgw)  
- Save routes ✅  

![Private Route Table with NAT Gateway 1](img/25.png)  
![Private Route Table with NAT Gateway 2](img/26.png)  
![Private Route Table with NAT Gateway 3](img/27.png)

### Step 2: Launch EC2 Instance 💻

Navigated to the **EC2 Dashboard** and clicked **Launch Instance**.  
![EC2 Dashboard Launch](img/29.png)

---

## Step 2.1: Launch EC2 in Public Subnet 🌐

- **Instance Name:** test-pub-ec2  
- **AMI:** Amazon Linux  
- **Instance Type:** t2.micro  
- **Key Pair:** test-nat-key  
- **Network / Subnet:** test-pub-subnet-01  
- **Auto-assign Public IP:** Enabled  

### Security Group 🔒
- **SSH (TCP 22):** 0.0.0.0/0  
- **HTTP (TCP 80):** 0.0.0.0/0  

Kept all other settings default and clicked **Launch Instance** ✅  

![Public EC2 Launch Screenshot 1](img/30.png)  
![Public EC2 Launch Screenshot 2](img/31.png)  
![Public EC2 Launch Screenshot 3](img/32.png)  
![Public EC2 Launch Screenshot 4](img/33.png)

## Step 2.2: Launch EC2 in Private Subnet 🔒

- **Instance Name:** test-pvt-ec2  
- **AMI:** Amazon Linux  
- **Instance Type:** t2.micro  
- **Network / Subnet:** test-pvt-subnet-01  

### Security Group 🛡️
- **SSH (TCP 22):** Anywhere (0.0.0.0/0)  
- **All Traffic:** Custom, Source 10.0.0.0/16  

✅ EC2 instance successfully launched in the **private subnet**.  
![Private EC2 Launch Screenshot 1](img/34.png)  
![Private EC2 Launch Screenshot 2](img/35.png)


## Step 3: Connect to Public EC2 via SSH 🖥️

- Used an **SSH client** to connect to the **public EC2 instance**.  
- Navigated to the **Downloads folder** where **test-nat-key.pem** is saved.  
- **Set proper permissions** for the key:  

```bash
chmod 400 test-nat-key.pem
ssh -i "test-nat-key.pem" ec2-user@<Public-EC2-IP>
```
![Launch Private EC2 Screenshot](img/36.png)
![Launch Private EC2 Screenshot](img/t1.png)

## Step 3.1: Verify Internet Access from Public EC2 🌐

- After logging into the **public EC2 instance**, checked **internet connectivity** using the `ping` command:  

```bash
ping -c 4 google.com
```
![Launch Private EC2 Screenshot](img/t2.png)

## Step 3.2: Save Key on Public EC2 (Why We Did This 🔑)

- To connect to the **private EC2 instance**, direct internet access is not available.  
- Therefore, we use the **public EC2 instance** as a **bastion/jump host**.  
- Copied the **PEM key** to the public EC2 and saved it securely.  
- This key can later be used with **SSH agent** or **direct SSH** to access the private EC2 instance.  

✅ Saving the key on the public EC2 ensures **secure access** to the private subnet EC2.  
![Save Key on Server Screenshot](img/t3.png)

## Step 4: Connect to Private EC2 via Public EC2 (Bastion) 🛡️

- Used an **SSH client** to connect to the **private EC2 instance** through the **public EC2 (bastion host)**.  
- **Set proper permissions** for the key and connected:  

```bash
chmod 400 test-nat-key.pem
ssh -i "test-nat-key.pem" ec2-user@<Private-EC2-Private-IP>
```
![Save Key on Server Screenshot](img/37.png)
![Save Key on Server Screenshot](img/t4.png)

## Step 4.1: Verify Internet Access from Private EC2 🌐🔒

- After logging into the **private EC2 instance**, checked **internet connectivity** using the `ping` command:  

```bash
ping -c 4 google.com
```
![Save Key on Server Screenshot](img/t5.png)











