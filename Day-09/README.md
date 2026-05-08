# ☁️ AWS VPC Setup for Load Balancer Demo

## 🚀 Step 1: VPC Creation

আমি AWS Console এ গিয়ে VPC Dashboard এ প্রবেশ করি। তারপর **Create VPC → VPC and more** অপশন ব্যবহার করে একটি নতুন VPC তৈরি করি।

## ⚙️ VPC Configuration

- 🏷️ Name: `load-balancer-demo`
- 🌐 IPv4 CIDR: `10.0.0.0/16`
- 🧾 Tenancy: Default
- 🌍 Availability Zones: 2
- 📡 Public Subnets: 2
- 🔒 Private Subnets: 0
- 🚫 NAT Gateway: None
- 🚫 VPC Endpoint: None

## ✅ Result

VPC সফলভাবে তৈরি হয়েছে।

- ✔️ 2 টি Availability Zone এ 2 টি Public Subnet তৈরি হয়েছে
- 🌐 Internet Gateway (IGW) attach হয়েছে
- 🛣️ Route Table (RT) তৈরি ও configure হয়েছে

## 📸 Screenshots

![VPC Setup](img/1.png)

![Public Subnets](img/2.png)

![Internet Gateway](img/3.png)

![Route Table](img/4.png)

---

# 🖥️ AWS EC2 Instance Setup for Load Balancer

## 🚀 Step 2: EC2 Instance Creation

আমি AWS Console এর EC2 Dashboard এ গিয়ে **Launch Instance** ব্যবহার করে দুটি EC2 instance তৈরি করেছি।

---

## 🖥️ Instance 1: load-balancer-server-a

### ⚙️ Configuration:
- 🏷️ Name: `load-balancer-server-a`
- 🐧 OS Image: Amazon Linux
- 💻 Instance Type: `t3.micro`
- 🔑 Key Pair: `load-balancer-demo`

### 🌐 Network Settings:
- ☁️ VPC: `load-balancer-demo`
- 🌍 Availability Zone: `us-east-2a`
- 📡 Subnet: Public Subnet (AZ-a)
- 🌐 Auto-assign Public IP: Enabled

### 🔐 Security Group:
- 🔑 SSH (22) → Source: `0.0.0.0/0`
- 🌐 HTTP (80) → Source: `0.0.0.0/0`

---

## 🖥️ Instance 2: load-balancer-server-b

### ⚙️ Configuration:
- 🏷️ Name: `load-balancer-server-b`
- 🐧 OS Image: Amazon Linux
- 💻 Instance Type: `t3.micro`
- 🔑 Key Pair: `load-balancer-demo`

### 🌐 Network Settings:
- ☁️ VPC: `load-balancer-demo`
- 🌍 Availability Zone: `us-east-2b`
- 📡 Subnet: Public Subnet (AZ-b)
- 🌐 Auto-assign Public IP: Enabled

### 🔐 Security Group:
- 🔑 SSH (22) → Source: `0.0.0.0/0`
- 🌐 HTTP (80) → Source: `0.0.0.0/0`

---

## 📸 Screenshots

![EC2 Step 3](img/7.png)

![EC2 Step 4](img/8.png)

![EC2 Step 5](img/9.png)

![EC2 Step 6](img/10.png)

![EC2 Step 7](img/11.png)

# 🖥️ EC2 Access & Nginx Setup (Load Balancer Backend Servers)

## 🚀 Step 3: SSH Access to EC2 Instances

আমি প্রথমে লোকাল terminal এ গিয়ে **Downloads folder** এ যাই, যেখানে `.pem` key file ছিল। এরপর key file এর permission secure করার জন্য chmod ব্যবহার করি এবং SSH দিয়ে দুইটি EC2 instance এ login করি।

---

## 🔐 Server Naming Setup

### 🖥️ Server A
- প্রথম EC2 instance এ login করার পর hostname পরিবর্তন করে `serverA` রাখা হয়  
- তারপর session থেকে বের হয়ে আবার SSH করে login করি যাতে terminal এ নামটা properly দেখা যায়  
- এতে করে বুঝতে সুবিধা হয় কোন server এ আছি

### 🖥️ Server B
- দ্বিতীয় EC2 instance এ একইভাবে hostname পরিবর্তন করে `serverB` রাখা হয়  
- আবার SSH করে login করে নিশ্চিত করা হয় hostname ঠিকভাবে apply হয়েছে  

---

## 👤 Root Access & System Update

- দুইটি server-এ root user access নেওয়া হয়  
- system update করে সব packages latest করা হয়  

---

## 🌐 Nginx Installation & Setup

### 🖥️ Server A
- Nginx install করা হয়  
- Nginx service start করা হয়  
- Nginx service enable করা হয় যাতে reboot এর পরেও চালু থাকে  

### 🖥️ Server B
- একইভাবে Nginx install করা হয়  
- service start করা হয়  
- service enable করা হয়  

---

## 📸 Screenshots

![Server A Setup 1](img/b1.png)

![Server A Setup 2](img/b2.png)

![Server A Setup 3](img/b3.png)

![Server A Setup 4](img/b4.png)

![Server B Setup 1](img/b5.png)

![Server B Setup 2](img/b6.png)

![Server B Setup 3](img/b7.png)

![Server B Setup 4](img/b8.png)

![Server B Setup 5](img/b9.png)

---

## 📌 Result

- ✔ দুইটি EC2 instance SSH দিয়ে access করা হয়েছে  
- ✔ Hostname set করা হয়েছে (serverA & serverB)  
- ✔ System update সম্পন্ন হয়েছে  
- ✔ Nginx install ও run করা হয়েছে  
- ✔ দুইটি server এখন web traffic serve করার জন্য ready  

---


