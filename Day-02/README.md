## Step 0: Choose AWS Region
AWS Management Console-এ লগইন করার পর **Region** হিসেবে **Ohio (us-east-2)** নির্বাচন করুন।  
সঠিক Region নির্বাচন করা গুরুত্বপূর্ণ, কারণ পরের সব resource সেই Region-এ তৈরি হবে।

![Select Region](img/region.png)

## Step 1: Open VPC Dashboard
আমরা **AWS Console**-এ **VPC** সার্চ করেছি এবং **VPC Dashboard**-এ প্রবেশ করেছি।  

![Search VPC](img/vpc.png)

### Step 1.1: Go to Create VPC
আমরা **VPC Dashboard**-এ গিয়ে **Create VPC** বাটনে ক্লিক করেছি।  

![Create VPC](img/vpcDashboard.png)

### Step 1.2: Create VPC
আমরা **Create VPC** ফর্মে নিম্নলিখিত সেটিং ব্যবহার করে একটি নতুন VPC তৈরি করেছি:  

- **VPC only** নির্বাচন করেছি  
- **Name:** `Test VPC`  
- **IPv4 CIDR block:** `192.168.0.0/16`  
- **No IPv6 CIDR block**  
- **VPC Encryption:** `Control: None`  
- **Tags:** `Name = test-vpc`  

এরপর **Create** বাটনে ক্লিক করেছি।  

![VPC Created](img/creatingvpc.png)



