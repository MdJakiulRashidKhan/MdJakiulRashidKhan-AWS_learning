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

# 💻 Step 5: Connect EC2 Instance & Mount EFS

After creating the EFS file system, I connected to my first EC2 instance to mount the shared storage.

---

## 🔑 SSH Access to EC2

Since the `.pem` key file was downloaded in the **Downloads** folder, I first navigated there:

- Used `cd Downloads`
- Changed permission of key file using `chmod 400`

This step ensured the private key is secure and usable for SSH connection.

Then I connected to the EC2 instance using SSH.

---

## 📊 Check Disk Space

After logging into the instance, I checked disk usage:

- Used `df -hT`

At this stage, the EFS storage was not yet mounted.

---

## 📁 Create Mount Directory

I created a directory for mounting EFS:

- `/storage-a`

This will act as the mount point for shared storage.

---

## 🔗 Mount EFS File System

Then I went to AWS EFS console:

- Opened `efs-shared-demo`
- Clicked on **Attach**
- Selected **NFS client instructions**
- Copied the provided mount command

On the EC2 instance, I pasted the command and mounted EFS to:

- `/storage-a`

---

## 📊 Verify Mount

After mounting, I again checked disk usage:

- `df -hT`

Now the EFS file system was successfully mounted and visible.

---

## 📂 Test File Creation

To confirm the shared storage is working:

- Navigated to `/storage-a`
- Created a file using `touch hello.tnx`
- Listed files using `ls`

The file was successfully created inside the EFS shared storage.

---

## 📸 Screenshots

![SSH Login](img/b1.png)

![Key Permission Setup](img/b2.png)

![Disk Check Before Mount](img/21.png)

![Create Mount Directory](img/22.png)

![EFS Attach Command](img/b3.png)

![Mounting EFS](img/b4.png)

![File System Verification](img/b5.png)

# 🔄 Step 6: Verify EFS Shared Storage on Second EC2 Instance

After successfully mounting EFS on the first EC2 instance, I moved to the second instance to confirm that the storage is shared properly.

---

## 🔑 SSH into Second EC2 Instance

I connected to the second EC2 instance (`efs-instance-b`) using the same process:

- Navigated to `Downloads` folder
- Set proper permission using `chmod 400` for the `.pem` file
- SSH into the instance successfully

---

## 📊 Check Existing Storage

After login, I checked disk usage:

- Used `df -hT`

At this point, the EFS storage was not yet mounted on this instance.

---

## 📁 Create Mount Directory

I created a new mount directory:

- `/storage-b`

This directory will be used to mount the shared EFS storage.

---

## 🔗 Mount EFS File System

Then I used the same NFS mount command from the EFS console:

- Copied the NFS client command
- Mounted it to `/storage-b`

---

## 📊 Verify Mount Status

After mounting, I checked again:

- Used `df -hT`

Now the EFS file system (`efs-demo`) was successfully mounted on this instance.

---

## 🔄 Verify Shared Storage

To confirm that storage is shared between both EC2 instances:

- Navigated to `/storage-b`
- Used `ls /storage-b`

I found the file:

- `hello.txt`

This confirmed that the file created from the first EC2 instance is visible in the second EC2 instance.

---

## 🎯 Final Result

✔ EFS is successfully mounted on both EC2 instances  
✔ Storage is shared between `efs-instance-a` and `efs-instance-b`  
✔ File synchronization is working correctly  

---

## 📸 Screenshots

![SSH to Instance B](img/b6.png)

![Key Permission Setup](img/b7.png)

![Disk Check Before Mount](img/b8.png)

![Create Mount Directory](img/b9.png)

![Mount EFS on Second Instance](img/b10.png)


# 🚀 AWS EFS Hands-on Project Conclusion

This project was a complete end-to-end implementation of Amazon Elastic File System (EFS) using AWS services, where I successfully designed the network architecture, configured security, launched compute resources, and validated shared storage functionality between multiple EC2 instances.

---

## 🏗️ Infrastructure Design

I started by building a custom networking environment using a VPC named **`efs-demo`**. The VPC was configured with a CIDR block of `10.0.0.0/16`, along with a public subnet, internet gateway, and route table. This setup ensured proper connectivity between resources inside the AWS environment.

This step helped me understand how AWS networking works in real-world scenarios, especially how resources communicate within a private cloud environment.

---

## 🛡️ Security Configuration

Next, I created a dedicated security group named **`efs-sg`** for the EFS service. I allowed **NFS traffic (TCP port 2049)** only from the VPC CIDR range (`10.0.0.0/16`) to ensure secure internal communication.

Additionally, I configured outbound rules to allow all traffic. This part strengthened my understanding of how security groups control access at the network level and how proper restriction ensures secure file sharing.

---

## 🖥️ Compute Resources (EC2 Instances)

After networking and security setup, I launched two EC2 instances:

- `efs-instance-a`
- `efs-instance-b`

Both instances were configured using Amazon Linux, `t3.micro` instance type, and the same key pair (`efs-demo-practice`). Public IPs were enabled for SSH access.

This allowed me to simulate a real multi-server environment where multiple machines need access to shared storage.

---

## 📂 EFS File System Creation

I then created an **Amazon Elastic File System (EFS)** named **`efs-dashboard-demo`** inside the same VPC (`efs-demo`).

During configuration:
- I selected the correct VPC
- Attached the security group `efs-sg`
- Used default file system policy
- Completed the setup to generate a unique File System ID

This step introduced me to AWS managed shared storage that automatically scales without manual intervention.

---

## 🔗 Mounting & Testing Shared Storage

### Instance A:
- Connected via SSH
- Created mount directory `/storage-a`
- Mounted EFS using NFS client command
- Verified using `df -hT`
- Created a test file `hello.txt`

### Instance B:
- Connected via SSH
- Created mount directory `/storage-b`
- Mounted same EFS file system
- Verified using `df -hT`
- Checked `/storage-b` and found `hello.txt`

This confirmed that both EC2 instances were successfully sharing the same storage volume in real time.

---

## 🎯 Final Outcome

Through this hands-on project, I achieved the following:

- Fully deployed AWS networking (VPC, subnet, route table, IGW)
- Configured secure communication using Security Groups
- Launched and connected multiple EC2 instances
- Created and configured AWS EFS file system
- Successfully mounted EFS on multiple servers
- Verified real-time shared storage functionality

---

## 💡 Key Learning

This project helped me deeply understand:

- How AWS EFS enables **centralized shared storage**
- How multiple EC2 instances can access the same file system simultaneously
- Importance of **NFS (port 2049)** in file sharing
- Role of VPC and security groups in controlling access
- Real-world architecture of scalable cloud storage systems

---

## 🚀 Final Thoughts

AWS EFS is a powerful solution for applications that require shared, scalable, and highly available storage. This hands-on practice gave me practical experience in cloud infrastructure design and reinforced my understanding of how distributed systems manage shared data efficiently across multiple compute instances.


