# 🌐 My AWS EC2 Launch Lab with Public and Private Subnets

In this project, I launched **EC2 instances** in both a **public subnet** and a **private subnet** using the AWS Console. I also explored the VPC wizard to quickly create VPC resources visually. By the end, my VPC had public and private resources ready to host applications! 🖥️☁️

**Part 4 in my networking series**
This assumes my previous networking projects have set up **NextWork VPC, Public Subnet, Private Subnet, Route Tables, and ACLs**.
I also used the Terraform files from [🌐 My AWS Private Subnet, Private Route Table, and Private Network ACL with Terraform](https://github.com/1suleyman/-My-AWS-Private-Subnet-Private-Route-Table-and-Private-Network-ACL-with-Terraform/tree/main?tab=readme-ov-file) to simplify subnet setup.

---

## 📋 Project Steps

### Step 1: Launch a Public EC2 Instance

**Goal:** Launch a web server in the public subnet to test internet access.

**Instructions:**

1. Navigate to **EC2 → Instances → Launch instances** in the AWS Console.
2. Name it `NextWork Public Server`.
3. Select **Amazon Linux 2023 AMI**.
4. Choose instance type: `t2.micro`.
5. Key pair: **Create new key pair** → Name: `NextWork key pair` → RSA `.pem` format.

💡 **Tip:** Key pairs enable SSH access. RSA is secure and widely supported. `.pem` is the standard private key format.

6. Network settings:

   * VPC: `Terraform VPC`
   * Subnet: Public Subnet
   * Security group: Select existing → `Terraform Networking series part 2 Security Group`

7. Click **Launch instance**.

8. Verify in **Networking** tab:

   * Public IPv4 address
   * Subnet
   * Availability Zone
   * VPC ID

✅ **Checkpoint:** Public EC2 instance launched successfully.

<img width="477" height="35" alt="Public EC2 Screenshot" src="https://github.com/user-attachments/assets/53e506f9-5948-4ed1-aecf-2f5b7823e76d" />

---

### Step 2: Launch a Private EC2 Instance

**Goal:** Launch a private EC2 instance that cannot be accessed directly from the internet.

**Instructions:**

1. Launch a new instance → Name: `NextWork Private Server`
2. AMI: Amazon Linux 2023
3. Instance type: `t2.micro`
4. Key pair: Use `NextWork key pair`

💡 **Tip:** You can reuse the same key pair for multiple instances. Keep it secure!

5. Network settings:

   * VPC: `Terraform VPC`
   * Subnet: `Terraform Private Subnet 1`
   * Security group: **Create new** → Name: `NextWork Private Security Group`
   * Inbound rules: SSH restricted to `NextWork Public Security Group`

💡 **Tip:** Restricting access to the public SG ensures only trusted public resources can connect.

6. Click **Launch instance**.

✅ **Checkpoint:** Private EC2 instance launched successfully.

<img width="296" height="59" alt="Private EC2 Screenshot" src="https://github.com/user-attachments/assets/e34997ee-e8a1-4645-ab82-47e78a9f40a9" />

---

### Step 3: Explore VPC Wizard for Quick Setup

**Goal:** Quickly visualize and create VPC resources.

**Instructions:**

1. Navigate to **VPC → Your VPCs → Create VPC → VPC and more**.
2. Observe the **VPC resource map**, showing:

   * Public and private subnets
   * Route tables
   * Internet gateway
   * Security groups

<img width="695" height="465" alt="VPC Resource Map Screenshot" src="https://github.com/user-attachments/assets/603560ab-9fe7-4d67-ae92-3e76bdea8306" />

3. Name tag auto-generation: enter `nextwork` → all resources are tagged automatically.
4. Review default CIDR blocks:

   * Public subnet: `10.0.0.0/24`
   * Private subnet: `10.0.1.0/24`

<img width="469" height="396" alt="Subnet CIDR Screenshot" src="https://github.com/user-attachments/assets/a0f483ad-3640-4e77-af77-5838043213b6" />

💡 **Tip:** Subnets cannot overlap within a VPC; multiple VPCs in a region can share CIDR blocks.

5. NAT gateways: None (to avoid charges).
6. Leave VPC endpoints unchecked (can add later).
7. Keep DNS options checked for human-readable hostnames.
8. Click **Create VPC** and watch the progress bar.
9. Verify **Resource Map** → confirm public subnet attached to route table and internet gateway.

✅ **Checkpoint:** VPC with public and private subnets successfully created.

<img width="240" height="399" alt="VPC Resource Map Screenshot" src="https://github.com/user-attachments/assets/39b5d266-251f-4624-b6f7-8fcf88ac2cdf" />

---

## 📌 Project Summary

| Step                        | Status | Key Notes                                                           |
| --------------------------- | ------ | ------------------------------------------------------------------- |
| Launch Public EC2 Instance  | ✅      | Public IPv4, security group allows HTTP/SSH from anywhere           |
| Launch Private EC2 Instance | ✅      | Private subnet, SSH restricted to public SG only                    |
| Explore VPC Wizard          | ✅      | Visualized all VPC resources and confirmed subnet and routing setup |

---

## 💡 Notes / Tips

* **Public vs. Private Subnets:** Public instances need internet access; private instances do not.
* **Security Groups:** Control inbound/outbound traffic for instances.
* **Key Pairs & SSH:** Keep private keys secure; reuse across instances if needed.
* **Resource Map:** Helps visualize all components in a single view.
* **NAT vs Internet Gateway:** NAT for private instances to access the internet; IGW for public instances to communicate outside.

---

## 📸 Screenshots

* Public EC2 instance launched and networking details
* Private EC2 instance with SSH restricted to public SG
* VPC resource map with public/private subnets, route tables, and IGW

---

## ✅ References

* [Launch Your EC2 Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)
* [Amazon VPC Wizard](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Scenario.html)
* [Key Pairs and SSH](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)
