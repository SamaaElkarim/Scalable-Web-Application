# Scalable-Web-Application
Scalable Web Application with ALB and Auto Scaling
# AWS Scalable Web Application Infrastructure (EC2-Based) 🚀

## 📌 Project Overview
This repository contains the complete documentation and architectural blueprint for a production-grade, highly available, and resilient web application infrastructure deployed on AWS. Designed according to the AWS Well-Architected Framework, this layout ensures strict security, automated scalability, and optimized global content delivery.

---

## 🗺️ Solution Architecture Diagram
Below is the architectural blueprint representing the traffic flow and component boundaries of the infrastructure:

![Solution Architecture Diagram](./architecture-diagram.png)

*Note: Traffic originates from Route 53, routes through CloudFront & WAF for protection and caching, enters the Application Load Balancer, and distributes dynamically to EC2 instances in private subnets across multiple AZs backed by a Multi-AZ RDS instance.*

---

## 🏗️ Technical Architecture & Key AWS Services

### 🌐 Networking & Core Infrastructure (VPC)
*   **VPC Architecture:** Configured across **two Availability Zones (AZs)** to eliminate single points of failure.
*   **Active VPC Verification:**
*   <img width="1105" height="46" alt="image" src="https://github.com/user-attachments/assets/31a99569-60d6-4bac-91d1-d4755e724b51" />

*   **Subnet Segmentation:** Strictly divided into **Public Subnets** (hosting the Application Load Balancer and NAT Gateways) and **Private Subnets** (hosting EC2 web servers and database instances) for data isolation.
*   **Traffic Management:** Network Access Control Lists (NACLs) and layered Security Groups act as firewalls. Outbound internet access for private instances is securely handled through **AWS NAT Gateways**.

### 💻 Compute, Routing & Dynamic Scaling
*   **Application Load Balancer (ALB):** Manages Layer 7 routing and performs automated target group health checks to direct traffic only to healthy instances.
*   **Auto Scaling Group (ASG):** Utilizes custom **Launch Templates** with automated user data scripts. Implements **Target Tracking Scaling Policies** to automatically scale the EC2 fleet based on real-time metrics (e.g., maintaining 60% average CPU load).
*   **Amazon CloudFront & Route 53:** Route 53 leverages Alias records pointing to CloudFront. CloudFront serves as a global CDN layer to cache static assets, decreasing user latency and lowering origin backend stress.

### 🔒 Security, Management & Monitoring
*   **AWS WAF (Web Application Firewall):** Shielding the ALB against common web exploits, enforcing rules covering the **OWASP Top 10 vulnerabilities** (SQLi, XSS, etc.).
*   **AWS Systems Manager (Session Manager):** Configured for highly secure, audited, and passwordless shell access to private EC2 instances, providing a **bastion-free alternative** that reduces open port vulnerabilities.
*   **Amazon CloudWatch & SNS:** Real-time metrics are consolidated into operational dashboards. CloudWatch Alarms are integrated with **Amazon SNS** to send automated email alerts during scaling actions or threshold breaches.

### 🗄️ Database Tier
*   **Amazon RDS Multi-AZ:** High-performance MySQL/PostgreSQL deployment leveraging synchronous replication to a standby instance in an alternative AZ. Provides automated failover capabilities to secure business continuity.

---

## 🎓 Learning Outcomes Achieved
Through architecting this project, deep engineering expertise was established in:
- [x] Designing secure custom VPCs with strict subnetting, explicit route table associations, and resilient NAT Gateway pathways.
- [x] Building high-availability infrastructure layouts capable of surviving Availability Zone outages.
- [x] Setting up sophisticated ALB listener configurations and target group monitoring parameters.
- [x] Coding dynamic Auto Scaling automation via target tracking and step scaling policies.
- [x] Hardening application infrastructure via integrated AWS WAF layers, isolation in private subnets, and locked-down Security Groups.
- [x] Eliminating the need for internet-facing Bastion/Jump hosts through AWS Systems Manager Session Manager integration.

---

## 👤 Author
* **Your Name** - [Your LinkedIn Profile](https://linkedin.com) | [Your Portfolio](your-portfolio-link)
