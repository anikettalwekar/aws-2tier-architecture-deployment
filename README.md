# AWS 2-Tier Architecture Deployment (Real-World Project)

### Author: [Aniket Talwekar]()
Role: AWS & DevOps Engineer | Experience: 3+ Years  
Domain: Cloud Infrastructure, Automation & Deployment  

---

## Project Overview

This project demonstrates the end-to-end deployment of a 2-Tier Web Application Architecture on AWS, implementing real-world production practices for security, scalability, and availability.

The architecture hosts a PHP web application connected to a MySQL RDS database, deployed inside a custom AWS VPC with private and public subnets across multiple Availability Zones.

This setup represents how modern organizations deploy web applications with load balancing, auto scaling, and HTTPS security using AWS-managed services.

---

## Architecture Diagram

<p align="center">
  <img src="docs/architecture-diagram.png" alt="AWS 2-Tier Architecture Diagram" width="700">
</p>

---

## AWS Services Used

| Layer | AWS Service | Purpose |
|-------|--------------|----------|
| Networking | VPC, Subnets, IGW, NAT | Network isolation and routing |
| Security | Security Groups, IAM, ACM | Controlled access and SSL |
| Compute | EC2, Auto Scaling, Launch Template | Host application layer |
| Load Balancing | Application Load Balancer (ALB) | Distribute incoming traffic |
| Database | RDS (MySQL, Multi-AZ) | Managed relational database |
| DNS | Route 53 | Domain management (aniket123.shop) |
| Access | Bastion Host (Windows) | Secure access to private subnets |
| Monitoring | CloudWatch | Instance health, scaling triggers |

---

## Key Features

- Custom VPC – Multi-AZ setup with public and private subnets  
- Auto Scaling Group (ASG) – Scales EC2 instances automatically  
- Application Load Balancer (ALB) – Handles traffic and SSL termination  
- Amazon RDS (MySQL) – Secure database in private subnets  
- Route 53 + ACM – Custom domain (aniket123.shop) with HTTPS encryption  
- Bastion Host – Secure access to internal resources  
- CloudWatch Metrics – For monitoring and scaling policies  

---

## Security Implementation

- Web tier in private subnets (no direct internet access)  
- Bastion host for admin access (RDP restricted to my IP)  
- HTTPS enforced via ACM SSL certificate  
- Least privilege access through IAM and Security Groups  
- Database isolated, accessible only from the app layer  

---

## Domain and HTTPS Configuration

- Domain: aniket123.shop (purchased from GoDaddy)  
- Hosted Zone: Created in Route 53  
- A Record (Alias): Points to ALB DNS  
- ACM Certificate:  
  - Domain: aniket123.shop, *.aniket123.shop  
  - Validation: DNS (auto via Route 53)  
  - Status: Issued  
- ALB Listener Update:  
  - Added HTTPS (443) Listener  
  - Attached ACM Certificate  
  - Forwarded traffic to Target Group  
  - Redirected HTTP → HTTPS  

Application is now securely accessible at:  
https://aniket123.shop

---

## Database (Amazon RDS MySQL)

- Engine: MySQL 8.x  
- Instance Type: db.t3.micro  
- Multi-AZ: Enabled  
- Backup: 7 days retention  
- Security: Only accessible from App-SG  
- Connection tested via Bastion (MySQL Workbench)  
- Verified using CLI commands:  
  ```sql
  show databases;
  use mydb;
  select * from users;
