# AWS VPC Setup for Load Balancer Demo

## Step 1: VPC Creation

আমি AWS Console এ গিয়ে VPC Dashboard এ প্রবেশ করি। তারপর **Create VPC → VPC and more** অপশন ব্যবহার করে একটি নতুন VPC তৈরি করি।

## VPC Configuration

- Name: `load-balancer-demo`
- IPv4 CIDR: `10.0.0.0/16`
- Tenancy: Default
- Availability Zones: 2
- Public Subnets: 2
- Private Subnets: 0
- NAT Gateway: None
- VPC Endpoint: None

## Result

VPC সফলভাবে তৈরি হয়েছে।

- 2 টি Availability Zone এ 2 টি Public Subnet তৈরি হয়েছে
- Internet Gateway (IGW) attach হয়েছে
- Route Table (RT) তৈরি ও configure হয়েছে

## Screenshots

![VPC Setup](img/1.png)

![Public Subnets](img/2.png)

![Internet Gateway](img/3.png)

![Route Table](img/4.png)

# AWS EC2 Instance Setup for Load Balancer

## Step 2: EC2 Instance Creation

আমি AWS Console এর EC2 Dashboard এ গিয়ে **Launch Instance** ব্যবহার করে দুটি EC2 instance তৈরি করেছি।

---

## 🖥️ Instance 1: load-balancer-server-a

### Configuration:
- Name: `load-balancer-server-a`
- OS Image: Amazon Linux
- Instance Type: `t3.micro`
- Key Pair: `load-balancer-demo`

### Network Settings:
- VPC: `load-balancer-demo`
- Availability Zone: `us-east-2a`
- Subnet: Public Subnet (AZ-a)
- Auto-assign Public IP: Enabled

### Security Group:
- SSH (22) → Source: `0.0.0.0/0`
- HTTP (80) → Source: `0.0.0.0/0`

---

## 🖥️ Instance 2: load-balancer-server-b

### Configuration:
- Name: `load-balancer-server-b`
- OS Image: Amazon Linux
- Instance Type: `t3.micro`
- Key Pair: `load-balancer-demo`

### Network Settings:
- VPC: `load-balancer-demo`
- Availability Zone: `us-east-2b`
- Subnet: Public Subnet (AZ-b)
- Auto-assign Public IP: Enabled

### Security Group:
- SSH (22) → Source: `0.0.0.0/0`
- HTTP (80) → Source: `0.0.0.0/0`

---

## 📸 Screenshots

![EC2 Step 3](img/7.png)

![EC2 Step 4](img/8.png)

![EC2 Step 5](img/9.png)

![EC2 Step 6](img/10.png)

![EC2 Step 7](img/11.png)

---

