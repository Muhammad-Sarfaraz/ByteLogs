# AWS Guide

### EC2 (Elastic Compute Cloud)

### What is EC2?
- Virtual servers in AWS
- Scalable, pay-as-you-go
- Flexible OS, CPU, RAM, storage

### Why Use EC2?
- No hardware setup
- Scalable on demand
- Secure (Security Groups, IAM, VPC)
- Cost-effective and reliable

### How EC2 Works
- Runs on physical servers via Hypervisor/Nitro
- Allocates vCPU, RAM, ENI (network), and storage (EBS/instance store)
- Connected to VPC (private IP, optional public IP)
- Traffic: EC2 → ENI → Subnet → NAT/IGW → Internet
- Security: Security Groups, ACLs, IAM roles, Key Pairs
- Lifecycle: Launch → Boot → Running → Stop/Start → Terminate

### Common Use Cases
- Web Hosting / APIs
- Databases
- Big Data / Analytics
- Machine Learning / AI
- Dev/Test Environments
- Hybrid Cloud Extensions

### Architecture (ASCII Diagram)
       +----------------+
       |   EC2 Instance |
       |----------------|
       | Private IP     |
       | ENI            |
       | Security Group |
       +----------------+
                |
                v
       +----------------+
       |   VPC Subnet   |
       | Route Table    |
       | NAT / IGW      |
       +----------------+
                |
                v
            Internet / AWS Services

