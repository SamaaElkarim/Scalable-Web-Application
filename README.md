# Scalable-Web-Application
Scalable Web Application with ALB and Auto Scaling
# AWS Scalable Web Application Infrastructure (EC2-Based) 🚀

## 📌 Project Overview
This repository contains the complete documentation and architectural blueprint for a production-grade, highly available, and resilient web application infrastructure deployed on AWS. Designed according to the AWS Well-Architected Framework, this layout ensures strict security, automated scalability, and optimized global content delivery.

---

## 🗺️ Solution Architecture Diagram
Below is the architectural blueprint representing the traffic flow and component boundaries of the infrastructure:

<img width="967" height="464" alt="image" src="https://github.com/user-attachments/assets/d6700d09-8e7b-4179-9859-7b119c434bcc" />


*Note: Traffic originates from Route 53, routes through CloudFront & WAF for protection and caching, enters the Application Load Balancer, and distributes dynamically to EC2 instances in private subnets across multiple AZs backed by a Multi-AZ RDS instance.*

---

## 🏗️ Technical Architecture & Key AWS Services

### 🌐 Networking & Core Infrastructure (VPC)
*   **VPC Architecture:** Configured across **two Availability Zones (AZs)** to eliminate single points of failure.
*   **Active VPC Verification:**
*   <img width="1105" height="46" alt="image" src="https://github.com/user-attachments/assets/31a99569-60d6-4bac-91d1-d4755e724b51" />

*   **Subnet Segmentation:** Strictly divided into **Public Subnets** (hosting the Application Load Balancer and NAT Gateways) and **Private Subnets** (hosting EC2 web servers and database instances) for data isolation.
*   I have created two public subnets and two private subnets.
*   <img width="1097" height="106" alt="image" src="https://github.com/user-attachments/assets/ce95e6b7-4da4-482c-8505-af1d6a199596" />
*   <img width="1091" height="115" alt="image" src="https://github.com/user-attachments/assets/3ae0ac70-59e0-42c8-9e76-7030cdb78766" />

*   **Traffic Management:** Network Access Control Lists (NACLs) and layered Security Groups act as firewalls. Outbound internet access for private instances is securely handled through **AWS NAT Gateways**.

### 💻 Compute, Routing & Dynamic Scaling
### 💻 Compute & Dynamic Scaling (EC2 + ASG)
*   **EC2 Instances:** Production-grade Virtual Servers hosting the web application. Deployed using **Amazon Linux 2** and initialized with custom automated User Data scripts to configure the web server environment upon launch.
*   **Launch Templates:** Standardized configuration templates that define instance types, AMI IDs, key pairs, and security groups to ensure consistent and unified EC2 deployments.
*   **Auto Scaling Group (ASG):** Spans across multiple Availability Zones to manage the EC2 fleet dynamically. Implements **Target Tracking Scaling Policies** to automatically scale instances up or down based on traffic load (e.g., maintaining average CPU load at 60%).
**Active EC2 Instances Verification:**
<img width="1097" height="118" alt="image" src="https://github.com/user-attachments/assets/a1b590c7-655f-4bf4-bbb0-c520285ce9f4" />

*   **Application Load Balancer (ALB):** Manages Layer 7 routing and performs automated target group health checks to direct traffic only to healthy instances.
*   <img width="1103" height="79" alt="image" src="https://github.com/user-attachments/assets/7664c560-7284-48c5-9e45-3e27b579e8a8" />
*   **Auto Scaling Group (ASG):** Utilizes custom **Launch Templates** with automated user data scripts. Implements **Target Tracking Scaling Policies** to automatically scale the EC2 fleet based on real-time metrics (e.g., maintaining 60% average CPU load).
*   <img width="1092" height="54" alt="image" src="https://github.com/user-attachments/assets/f91452a7-64f6-451d-84a2-5e2054f91906" />
*   **Amazon CloudFront & Route 53:** Route 53 leverages Alias records pointing to CloudFront. CloudFront serves as a global CDN layer to cache static assets, decreasing user latency and lowering origin backend stress.

### 🔒 Security, Management & Monitoring
*   **AWS WAF (Web Application Firewall):** Shielding the ALB against common web exploits, enforcing rules covering the **OWASP Top 10 vulnerabilities** (SQLi, XSS, etc.).
*   **AWS Systems Manager (Session Manager):** Configured for highly secure, audited, and passwordless shell access to private EC2 instances, providing a **bastion-free alternative** that reduces open port vulnerabilities.
*   **Amazon CloudWatch & SNS:** Real-time metrics are consolidated into operational dashboards. CloudWatch Alarms are integrated with **Amazon SNS** to send automated email alerts during scaling actions or threshold breaches.
*   <img width="1058" height="441" alt="image" src="https://github.com/user-attachments/assets/a8b9eec8-4c41-4cb1-960a-e1fa6b258971" />
An email alert is triggered when the CPU utilization exceeds a predefined threshold.

### 🗄️ Database Tier
*   **Amazon RDS Multi-AZ:** High-performance MySQL/PostgreSQL deployment leveraging synchronous replication to a standby instance in an alternative AZ. Provides automated failover capabilities to secure business continuity.
<img width="1068" height="55" alt="image" src="https://github.com/user-attachments/assets/695970d8-6d22-4946-b333-855a114ee926" />

---

## 🎓 Learning Outcomes Achieved
Through architecting this project, deep engineering expertise was established in:
- [x] Designing secure custom VPCs with strict subnetting, explicit route table associations, and resilient NAT Gateway pathways.
- [x] Building high-availability infrastructure layouts capable of surviving Availability Zone outages.
- [x] Setting up sophisticated ALB listener configurations and target group monitoring parameters.
- [x] Coding dynamic Auto Scaling automation via target tracking and step scaling policies.
- [x] Hardening application infrastructure via integrated AWS WAF layers, isolation in private subnets, and locked-down Security Groups.
- [x] Eliminating the need for internet-facing Bastion/Jump hosts through AWS Systems Manager Session Manager integration.

Project Video
Kindly check video at release
<img width="378" height="132" alt="image" src="https://github.com/user-attachments/assets/870cd6c3-c902-4b4e-a8b4-5c4ec435777e" />

