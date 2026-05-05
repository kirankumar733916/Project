# AWS Highly Available 3-Tier Architecture 🚀

## 📌 Overview

This project demonstrates the design and implementation of a **highly available, scalable, and secure 3-tier web application architecture on AWS**. The architecture follows AWS best practices, including **multi-AZ deployment, network isolation, load balancing, and fault tolerance**.

It is designed to simulate a **production-grade environment** suitable for modern web applications.

---

## 🏗️ Architecture Summary

The system is deployed in a single VPC across two Availability Zones (`ap-south-1a`, `ap-south-1b`) with clear separation of concerns:

* **Presentation Layer**
* **Application Layer (Compute + Auto Scaling)**
* **Data Layer (Database + Failover)**

---

## 🌐 Architecture Components

### 1. Networking Layer

* VPC (`10.0.0.0/16`)
* 2 Availability Zones for high availability
* Subnets:

  * Public Subnets (ALB, NAT Gateway)
  * Private Subnets (EC2, RDS)

---

### 2. Edge & Content Delivery

* Amazon CloudFront (CDN)
* Amazon S3 (static content storage)
* Amazon Route 53 (DNS routing)

**Behavior Routing:**

* `/static/*` → S3
* `/api/*` → Application Load Balancer

---

### 3. Load Balancing

* Internet-facing **Application Load Balancer (ALB)**
* Distributes traffic across EC2 instances in multiple AZs
* Health checks ensure traffic is sent only to healthy instances

---

### 4. Compute Layer

* EC2 instances deployed in **private subnets**
* Managed by **Auto Scaling Group**
* Automatically scales based on demand

---

### 5. Data Layer

* Amazon RDS (Multi-AZ deployment)

  * Primary DB in AZ-1
  * Standby DB in AZ-2 (automatic failover)
* Securely accessible only from application layer

---

### 6. Security

* Security Components in Architecture

  * Certificate Manager (ACM)
  * Secret Manager
  * Key Management Service (KMS)
* These components ensure secure communication, credential protection, and encryption at rest/in transit.

* Security Groups:

  * ALB → EC2 (HTTP/HTTPS only)
  * EC2 → RDS (DB port only e.g 3306 or 5432)
* No public access to EC2, RDS
* IAM roles for secure service access
* AWS Systems Manager (SSM) for instance access (no SSH)

---

### 7. Internet Access

* Internet Gateway attached to VPC
* NAT Gateway in each public subnet
* Private subnets route outbound traffic via NAT

---

### 8. Monitoring & Logging

* Amazon CloudWatch:

  * Metrics
  * Logs
  * Alarms

---

## 🔁 Traffic Flow

1. User sends request via browser
2. Route 53 resolves domain
3. CloudFront serves cached content or forwards request
4. ALB receives request and routes to EC2 instances
5. EC2 processes request and interacts with:

   * RDS (database)
6. Response is returned via ALB → CloudFront → User

---

## ⚙️ Key Features

* High Availability (Multi-AZ)
* Auto Scaling for compute resources
* Secure private networking
* CDN for low latency delivery
* Managed database with failover
* Infrastructure aligned with AWS Well-Architected Framework

---

## 🧠 Design Decisions

* **Single VPC** used to reduce latency and simplify networking
* **Private subnets for compute and database** to enhance security
* **CloudFront + S3** for efficient static content delivery
* **NAT Gateway per AZ** to ensure fault-tolerant outbound access
* **SSM instead of Bastion Host** for secure instance access

---

## 🚀 Future Enhancements

* Plan to implement CI/CD pipelines using GitHub Actions, AWS CodePipeline, and Jenkins
* Automate infrastructure provisioning with AWS CloudFormation
* Plan to containerize applications using Amazon ECS, Docker
* Will secure applications using AWS WAF for DDoS protection
* Aim to improve performance and reduce latency using Amazon ElastiCache
* Plan to configure Amazon SNS and SQS for reliable alerting and asynchronous messaging
* Will implement Transit Gateway to connect multiple VPCs and use VPC peering for two-VPC connectivity

---

## 📊 Skills Demonstrated

* AWS Networking (VPC, Subnets, Routing)
* Load Balancing (ALB)
* Compute Scaling (Auto Scaling Groups)
* Database Management (RDS Multi-AZ)
* CDN & DNS (CloudFront, Route 53)
* Security Best Practices (IAM, SG, SSM, KMS, ACM, Secret Manager)
* Monitoring (CloudWatch)

---

## 📎 Conclusion

This project showcases a **real-world AWS architecture** that balances **scalability, security, and high availability**, making it suitable for production workloads and demonstrating strong cloud engineering fundamentals.

---
