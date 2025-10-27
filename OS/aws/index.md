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


### S3 (Simple Storage Service)
S3 (Simple Storage Service) is AWS’s object storage service.

Each object has:
- Data: raw file bytes → stored in distributed storage across multiple AWS data centers / Availability Zones (AZs).
- Key: unique identifier for the object → stored in AWS’s internal indexing system, not inside the file itself.
- Metadata: system metadata (content-type, size) + user-defined metadata → also stored in AWS’s internal system, separately from the raw bytes.

```
Object = [Key + Data (your file bytes) + Metadata]

[Your File Upload]
       |
       v
  +-----------------------+
  |       S3 Bucket       |
  |-----------------------|
  | Key: myfile.exe       |  <-- stored in AWS index
  | Data: raw file bytes  |  <-- stored in distributed storage
  | Metadata:             |  <-- stored in AWS internal metadata store
  |  - Content-Type       |
  |  - Size               |
  |  - User-defined tags  |
  +-----------------------+
       |
       v
AWS uses the Key to locate Data and Metadata when accessed
```

### EBS (Elastic Block Store)
EBS (Elastic Block Store) = AWS’s block-level storage service,Think of it as a virtual hard drive in the cloud, Designed to attach to EC2 instances, Even if EC2 stops, data on EBS can persist.

Multiple Volume Types
- General Purpose SSD (gp3/gp2) → everyday workloads
- Provisioned IOPS SSD (io2/io2 Block Express) → high-performance DBs
- Magnetic / Cold HDD → infrequent access or throughput-oriented workloads

```
[EC2 Instance]
       |
       v
  +----------------+
  |    EBS Volume  |
  |----------------|
  | Raw Block Data |
  | Replicated in |
  | 1 AZ          |
  +----------------+
       |
       v
     Persistent Storage (even if EC2 stops)

```

