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

![img1](./img/1.png)  
![img2](./img/2.png)  
![img3](./img/3.png)  
![img4](./img/4.png)

# 🖥️ Step 2: Launch EC2 Instance (EBS Demo)

## 📌 Overview
In this step, I launched an EC2 instance inside the custom VPC to use it for EBS practice and configuration.

---

## 🚀 Launch EC2 Instance

I went to the **EC2 Dashboard** and clicked on **Launch Instance**.

---

## ⚙️ Instance Configuration

- **Instance Name:** ec2-1-ebs-demo  
- **AMI (OS Image):** Ubuntu  
- **Instance Type:** t3.micro  
- **Key Pair:** ebs-demo key pair  

---

## 🌐 Network Settings

- **VPC:** jakiul-ebs-vpc (custom VPC)  
- **Subnet:** Public Subnet  
- **Auto-assign Public IP:** Enabled  

---

## 🔐 Security Group Configuration

- **Inbound Rule:**
  - SSH (Port 22)
  - Source: 0.0.0.0/0

---

## 💾 Storage

- Default storage configuration used

---

## 🖼️ Screenshots

![img5](./img/5.png)  
![img6](./img/6.png)  
![img7](./img/7.png)  
![img8](./img/8.png)  
![img9](./img/9.png)

## 🔑 SSH Access & Setup

After downloading the key pair file, I moved it to the **Downloads** folder.

Then I changed permission of the PEM file using `chmod 400 ebs-demo.pem`.

After that, I connected to the EC2 instance using SSH with the public IP.

---

## 💽 Disk Check

After login to the instance, I checked the attached storage using `lsblk`.

I found that an **8 GB root volume** was attached to the instance.

---

## 🖼️ Screenshots

![b1](./img/b1.png)  
![b2](./img/b2.png)  
![b3](./img/b3.png)

# 💽 Step 3: Create EBS Volume

## 📌 Overview
In this step, I created an **Amazon EBS Volume** from the EC2 Dashboard under Elastic Block Store (EBS) section.

---

## 🚀 Go to EBS Volumes

I navigated to:

**EC2 Dashboard → Elastic Block Store → Volumes → Create Volume**

---

## ⚙️ Volume Configuration

- **Volume Type:** gp3  
- **Size:** 100 GiB  
- **IOPS:** 3000  
- **Throughput:** 125 MiB/s  
- **Availability Zone:** us-east-2a (same as EC2 instance)  
- **Snapshot ID:** Not selected (created new volume)

---

## 🧾 Create Volume

After configuring all settings, I clicked on **Create Volume**.

The volume was successfully created and is now available for attachment.

---

## 🖼️ Screenshots

![img10](./img/10.png)  
![img11](./img/11.png)  
![img12](./img/12.png)  
![img13](./img/13.png)

# 🔗 Step 4: Attach EBS Volume to EC2 Instance

## 📌 Overview
In this step, I attached the previously created EBS volume to my EC2 instance for storage usage.

---

## 💽 Volume Details

- **Volume Name:** ebs-1-100-gb  
- **Volume Type:** gp3  
- **Size:** 100 GiB  

---

## 🚀 Attach Volume Process

I selected the created volume and clicked:

**Actions → Attach Volume**

---

## ⚙️ Attachment Configuration

- **Instance:** ec2-1-ebs-demo  
- **Device Name:** /dev/sdk  

Then I clicked **Attach Volume** to complete the process.

---

## 🖼️ Screenshots

![img14](./img/14.png)  
![img15](./img/15.png)

## 🧠 Disk Verification

After connecting to the EC2 instance:

- I checked disk partitions using `sudo fdisk -l`  
  → A new **100 GB disk** was visible  

- Then I checked the filesystem using `sudo file -s /dev/nvme1n1`  
  → Output showed **data**

👉 This means the volume had no filesystem yet.

---

## ⚙️ Format the Volume

- I created a filesystem using `sudo mkfs -t xfs /dev/nvme1n1`  

👉 XFS is used because it provides high performance and is widely used in cloud systems.

- Verified again using `sudo file -s /dev/nvme1n1`  
  → Output showed **XFS filesystem**

---

## 📁 Mount the Volume

- Created a directory: `/myebsvol`  
- Mounted the volume to that directory  

- Checked using `ls -lart /myebsvol`  

👉 This confirms the mount point is working correctly.

---

## 📊 Verify Storage

- Checked disk usage using `df -h`  

👉 This ensures the 100 GB EBS volume is successfully mounted.

---

## 📂 File Operations

- Navigated to `/myebsvol`  
- Checked files using `ls` → directory was empty  

👉 Because it is a new volume

- Created two files:
  - `1.txt`
  - `2.txt`  

---

## 🖼️ Screenshots

![b4](./img/b4.png)  
![b6](./img/b6.png)  
![b7](./img/b7.png)  
![b8](./img/b8.png)  
![b9](./img/b9.png)  
![b10](./img/b10.png)  
![b11](./img/b11.png)

# 🖥️ Step 5: Launch 2nd EC2 Instance (Same Region)

## 📌 Overview
In this step, I launched a second EC2 instance in the same region to use the existing EBS volume with another instance.

---

## 🚀 Launch EC2 Instance

I went to the **EC2 Dashboard** and clicked on **Launch Instance**.

---

## ⚙️ Instance Configuration

- **Instance Name:** ec2-2-ebs-demo  
- **AMI (OS Image):** Ubuntu  
- **Instance Type:** t3.micro  
- **Key Pair:** ebs-demo  

---

## 🌐 Network Settings

- **Region:** Same as previous EC2 and EBS  
- **VPC:** jakiul-ebs-vpc  
- **Subnet:** Public Subnet  
- **Auto-assign Public IP:** Enabled  

---

## 🔐 Security Group

- **Inbound Rule:**
  - SSH (Port 22)  
  - Source: 0.0.0.0/0  

---

## 💾 Storage

- Default storage configuration used  

---

## 🚀 Launch

After keeping all other settings default, I successfully launched the second EC2 instance.

---

## 🖼️ Screenshots

![img16](./img/16.png)  
![img17](./img/17.png)  
![img18](./img/18.png)  
![img19](./img/19.png)

## 🔑 SSH Access & Verification

After downloading the key pair:

- I changed permission using `chmod 400 ebs-demo.pem`  
- Then I connected to the instance using SSH  

After login:

- I checked disks using `lsblk`  
- Only the default **8 GB root volume** was visible  

👉 This confirms that the previously created 100 GB EBS volume is not attached to this instance yet.

---

## 🖼️ Screenshots

![b12](./img/b12.png)

# 📸 Step 6: EBS Snapshot, Restore & Data Verification

## 📌 Overview
In this step, I created a snapshot of the EBS volume, restored a new volume from that snapshot, attached it to another EC2 instance, and verified the data.

---

## 📸 Create Snapshot

EC2 Dashboard → Volumes → Select **ebs-1-100-gb**

- Actions → Create Snapshot  
- Description: ebs-1-ec2-1-1-2-txt-file  

Snapshot created successfully.

---

## 🔁 Create Volume from Snapshot

EC2 Dashboard → Snapshots

- Select snapshot  
- Actions → Create Volume from Snapshot  

### ⚙️ Configuration

- Default settings  
- Tag:
  - Key: name  
  - Value: ebs-from-snap-1  

Volume created successfully.

---

## 🔗 Attach Volume to EC2-2

- Renamed volume: **ebs-2-100-gb**  
- Actions → Attach Volume  

### ⚙️ Configuration

- Instance: ec2-2-ebs-demo  
- Device Name: /dev/sdk  

Volume attached successfully.

---

## 🖼️ EC2 Screenshots

![img20](./img/20.png)  
![img21](./img/21.png)  
![img22](./img/22.png)  
![img23](./img/23.png)  
![img24](./img/24.png)  
![img25](./img/25.png)  

---

## 💽 Disk Check (EC2-2)

- Checked using `lsblk` → 100 GB disk found  
- Checked using `sudo file -s /dev/nvme1n1` → XFS filesystem  

---

## 📁 Mount & Verify Data

- Created directory: `/myebsvol2`  
- Mounted volume  

- Checked files using `ls /myebsvol2`  

👉 Found:
- 1.txt  
- 2.txt  

---

## 🖼️ Bash / Terminal Screenshots

![b13](./img/b13.png)  
![b14](./img/b14.png)  
![b15](./img/b15.png)

# 🌏 Step 7: Create VPC in Another Region (Singapore)

## 📌 Overview
In this step, I created a new VPC in another region (Singapore) to use the EBS snapshot in a different region.

---

## 🌍 Switch Region

I changed the AWS region to **Singapore**.

---

## 🏗️ Create VPC

I went to the **VPC Dashboard** and clicked on **Create VPC**.

Then selected **VPC and More** option.

---

## ⚙️ VPC Configuration

- **VPC Name:** ebs-snap  
- **IPv4 CIDR Block:** 10.0.0.0/16  
- **Tenancy:** Default  

---

## 🌐 Subnet Configuration

- **Availability Zone:** 1  
- **Public Subnet:** 1  
- **Private Subnet:** 1 (0 দিলেও সমস্যা নেই)  

---

## 🔗 Networking Setup

- **NAT Gateway:** None  
- **VPC Endpoint:** None  

---

## 🚀 Result

After creating the VPC, the following resources were automatically created:

- 1 VPC  
- Public Subnet  
- Private Subnet  
- Internet Gateway (IGW) attached  
- Route Table configured  

---

## 🖼️ Screenshots

![img26](./img/26.png)  
![img27](./img/27.png)  
![img28](./img/28.png)  
![img29](./img/29.png)

# 🖥️ Step 8: Launch EC2 Instance in Singapore Region

## 📌 Overview
In this step, I launched a new EC2 instance in the Singapore region to work with the migrated EBS snapshot setup.

---

## 🚀 Launch EC2 Instance

I went to the **EC2 Dashboard** in Singapore region and clicked **Launch Instance**.

---

## ⚙️ Instance Configuration

- **Instance Name:** ec2-3-ebs-demo  
- **AMI (OS Image):** Ubuntu  
- **Instance Type:** t3.micro  
- **Key Pair:** ebs-demo-2  

---

## 🌐 Network Settings

- **VPC:** ebs-snap-vp  
- **Subnet:** Public Subnet  
- **Auto-assign Public IP:** Enabled  

---

## 🔐 Security Group

- Created new Security Group  
- **Inbound Rule:**
  - SSH (Port 22)
  - Source: 0.0.0.0/0  

---

## 🚀 Launch

After keeping all settings, I launched the EC2 instance successfully.

---

## 🖼️ EC2 Screenshots

![img30](./img/30.png)  
![img31](./img/31.png)  
![img32](./img/32.png)  
![img33](./img/33.png)

---

## 🔑 SSH Access & Setup

After downloading the PEM file:

- I navigated to the **Downloads** folder  
- Changed permission using `chmod 400 ebs-demo-2.pem`  
- Connected to EC2 instance using SSH  

---

## 💽 Disk Verification

After login to the instance:

- Checked disks using `lsblk`  
- Found only **8 GB root volume**

---

## 🖼️ Bash Screenshot

![b16](./img/b16.png)



# 🌎 Step 9: Cross-Region Snapshot Copy (Ohio → Singapore) & Restore

## 📌 Overview
In this step, I copied an EBS snapshot from Ohio region to Singapore region, created a new volume, attached it to EC2, and verified data persistence.

---

## 📸 Copy Snapshot to Another Region

I went to:

EC2 Dashboard → Snapshots (Ohio Region)

- Selected snapshot: **ebs-1-ec2-1-1-2-txt-file**
- Clicked: **Actions → Copy Snapshot**

### ⚙️ Configuration

- **Description:** ebs-1-ec2-1-1-2-txt-file-ohio-to-singapore  
- **Destination Region:** ap-southeast-1 (Singapore)

Then I copied the snapshot successfully.

---

## 🔁 Create Volume from Snapshot (Singapore)

In Singapore region:

EC2 Dashboard → Snapshots

- Selected copied snapshot  
- Clicked: **Actions → Create Volume from Snapshot**

### ⚙️ Configuration

- **Availability Zone:** same as EC2 instance  
- Default settings used  

Volume created successfully.

---

## 🔗 Attach Volume to EC2

- Selected volume  
- Clicked: **Actions → Attach Volume**

### ⚙️ Configuration

- **Instance:** ec2-3-ebs-demo  
- **Device Name:** /dev/sdk  

Volume attached successfully.

---

## 🖼️ Screenshots

![img34](./img/34.png)  
![img35](./img/35.png)  
![img36](./img/36.png)  
![img37](./img/37.png)  
![img38](./img/38.png)  
![img39](./img/39.png)  
![img40](./img/40.png)

---

## 💽 Disk Verification (EC2-3)

After login to EC2:

- Checked disk using `lsblk`  
  → 100 GB disk found  

- Checked filesystem using `sudo file -s /dev/nvme1n1`  
  → XFS filesystem detected  

---

## 📁 Mount & Data Verification

- Created directory: `/myebsvol3`  
- Mounted volume using `sudo mount /dev/nvme1n1 /myebsvol3`  

- Verified files using `ls /myebsvol3`  

👉 Found:
- 1.txt  
- 2.txt  

---

## 🖼️ Bash Screenshots

![b17](./img/b17.png)  
![b18](./img/b18.png)  
![b19](./img/b19.png)

## 📌 Project Summary

This project demonstrates a complete AWS EBS workflow including VPC creation, EC2 instances setup, EBS volume creation, attachment, filesystem configuration, snapshot backup, and cross-region snapshot copy.

I created multiple EC2 instances and attached EBS volumes to store and manage data. Then I took snapshots of the volume, restored them in another region (Singapore), and verified data persistence by accessing files like `1.txt` and `2.txt` across instances.

This project shows real-world cloud storage management, backup strategy, and cross-region disaster recovery using AWS services.

## 👨‍💻 Author
Md. Jakiul Rashid Khan








