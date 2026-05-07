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
