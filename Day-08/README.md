# 🚀 AWS EFS Hands-on Practice – VPC Setup

Today I started my AWS EFS hands-on practice by creating a custom VPC environment.

---

## 🛠️ Step 1: Create VPC for EFS

First, I went to the AWS Management Console and opened the VPC Dashboard.

Then I clicked on:

- Create VPC
- Selected **VPC and more**

---

## 📌 VPC Configuration

| Setting | Value |
|---|---|
| VPC Name | `efs-demo` |
| IPv4 CIDR Block | `10.0.0.0/16` |
| Tenancy | `Default` |
| Availability Zones (AZs) | `1` |
| Public Subnets | `1` |
| Private Subnets | `0` |
| NAT Gateway | `None` |
| VPC Endpoints | `None` |

After completing all configurations, I clicked on **Create VPC**.

---

## ✅ Resources Automatically Created

After the VPC was created, AWS automatically created the following resources:

- ✅ 1 VPC
- ✅ 1 Public Subnet
- ✅ 1 Internet Gateway (IGW)
- ✅ 1 Route Table (RT)

---

## 📸 Screenshots

![VPC Create](img/1.png)

![VPC Created](img/2.png)

![Subnet and Route Table](img/3.png)

![Internet Gateway](img/4.png)

# 🛡️ Step 2: Create Security Group for EFS

After creating the VPC, I created a Security Group for AWS EFS.

First, I went to:

- EC2 Dashboard
- Security Groups
- Clicked on **Create Security Group**

---

## 📌 Security Group Configuration

| Setting | Value |
|---|---|
| Security Group Name | `efs-demo` |
| Description | `Allows EFS shared storage` |
| VPC | `efs-demo` |

---

## 📥 Inbound Rules

Since EFS uses the NFS protocol, I added an inbound rule with the following configuration:

| Type | Protocol | Port | Source |
|---|---|---|---|
| NFS | TCP | 2049 | `10.0.0.0/16` |

I only whitelisted my VPC subnet range so that instances inside the VPC can access the shared EFS storage securely.

---

## 📤 Outbound Rules

| Type | Destination |
|---|---|
| All Traffic | `0.0.0.0/0` |

After completing the configuration, I clicked on **Create Security Group**.

---

## 📸 Screenshots

![Create Security Group](img/5.png)

![Security Group Created](img/6.png)

# 🖥️ Step 3: Launch EC2 Instances for EFS

After creating the Security Group, I launched two EC2 instances to connect with the EFS shared storage.

First, I went to:

- EC2 Dashboard
- Clicked on **Launch Instance**

---

## 📌 EC2 Instance Configuration

I created two instances with the following names:

- `efs-instance-a`
- `efs-instance-b`

---

## ⚙️ Instance Settings

| Setting | Value |
|---|---|
| OS Image | Amazon Linux |
| Instance Type | `t3.micro` |
| Key Pair | `efs-demo-practice` |
| VPC | `efs-demo` |
| Public IP | Enabled |

---

## 🔐 Security Group Configuration

I created/used a Security Group and added an inbound SSH rule so I could connect to the instances remotely.

| Type | Port | Source |
|---|---|---|
| SSH | 22 | My IP |

After completing all configurations, I clicked on **Launch Instance**.

---

## 📸 Screenshots

![Launch Instance](img/7.png)

![Instance Configuration](img/8.png)

![Amazon Linux Selection](img/9.png)

![Network Settings](img/10.png)

![Security Group Configuration](img/11.png)

![Launch Summary](img/12.png)

![EC2 Instances Running](img/13.png)

# 📂 Step 4: Create AWS EFS File System

After launching EC2 instances, I moved to creating the shared storage using AWS EFS.

---

## 🛠️ Create File System

I went to:

- AWS Dashboard
- Opened **Elastic File System (EFS)**
- Clicked on **Create File System**

---

## 📌 File System Configuration

| Setting | Value |
|---|---|
| Name | `efs-dashboard-demo` |
| VPC | `efs-demo` |
| Configuration | Customize |

I selected **Customize** and kept the default settings for file system configuration.

Then I clicked **Next**.

---

## 🌐 Network Access Settings

In the network access section:

- Selected my Security Group: `efs-sg`
- Ensured it is attached to all required subnets inside the VPC

Then I clicked **Next**.

---

## 🔐 File System Policy

- Kept **Default policy**
- Proceeded with **Next**

---

## 🚀 Create File System

Finally, I clicked on **Create**.

After a few moments:

- The EFS file system was successfully created
- File System ID was generated
- This ID will be used to mount the storage in EC2 instances

---

## ✅ Result

- File System Name: `efs-shared-demo`
- Status: Active
- Ready to mount on EC2 instances

---

## 📸 Screenshots


![File System Settings](img/14.png)

![VPC Selection](img/15.png)

![Network Access](img/16.png)

![Security Group Selection](img/17.png)

![Policy Settings](img/18.png)

![Create Confirmation](img/19.png)

![EFS Created Successfully](img/20.png)
