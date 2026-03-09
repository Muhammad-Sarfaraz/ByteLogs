# Lightsail

## Overview
**Amazon Lightsail** is a simplified VPS service from Amazon Web Services (AWS).  
It provides virtual servers, storage, networking, and DNS with predictable monthly pricing.

Lightsail is designed for developers who want quick deployment without managing the full complexity of AWS infrastructure.

---

## Core Concept
Lightsail bundles multiple infrastructure components into a single service:

- Compute (VPS)
- Networking
- Storage
- DNS
- Snapshots
- Load Balancer

This makes it suitable for:
- Small production apps
- MVPs
- Development environments
- Personal projects

---

## Main Resources

### 1. Instance
A virtual machine running Linux or Windows.

Common blueprints:
- Ubuntu
- Debian
- Amazon Linux
- WordPress
- Node.js
- LAMP stack

Example plan:

RAM: 1 GB  
CPU: 1 vCPU  
Storage: 40 GB SSD  
Bandwidth: 2 TB transfer

---

### 2. Static IP
A permanent public IP that can be attached to an instance.

Use cases:
- Domain mapping
- Prevent IP change after restart

---

### 3. DNS Zone
Lightsail provides DNS management.

Typical DNS records:

| Record | Purpose |
|------|------|
| A | Domain → Server IP |
| CNAME | Subdomain mapping |
| MX | Email routing |

---

### 4. Block Storage
Additional disks attached to instances.

Used when:
- Application needs more storage
- Media or logs need separate storage

---

### 5. Snapshots
Backups of instances or disks.

Use cases:
- Server backups
- Cloning environments
- Disaster recovery

---

### 6. Load Balancer
Simple HTTP/HTTPS load balancer.

Features:
- Traffic distribution
- Health checks
- SSL termination

---

## Networking Model

Each instance has:

- Public IP
- Private IP
- Firewall configuration

Example firewall rules:

| Port | Purpose |
|----|----|
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| Custom | Application ports |

---

## Deployment Workflow

Typical deployment steps:

1. Create Lightsail instance
2. Attach static IP
3. Connect via SSH


ssh ubuntu@server-ip


4. Install runtime

Example:
- Node.js
- Docker
- Nginx

5. Deploy application

6. Configure domain DNS

---

## Common Use Cases

- Small production applications
- WordPress hosting
- Backend APIs
- Startup MVP
- Dev / staging environments

---

## Advantages

- Easy setup
- Predictable pricing
- Quick deployment
- Built-in DNS
- Integrated backups

---

## Limitations

- Limited scaling
- Fewer networking features compared to EC2
- Less infrastructure customization

---

## Lightsail vs EC2

| Feature | Lightsail | EC2 |
|------|------|------|
| Setup | Simple | Complex |
| Pricing | Fixed monthly | Pay-as-you-go |
| Networking | Basic | Advanced |
| Scalability | Limited | High |

---

## When to Use Lightsail

Use Lightsail when:

- You need a quick VPS
- Building an MVP
- Running small production systems
- Hosting personal or startup projects

Avoid Lightsail when:

- Large scale infrastructure is required
- Advanced networking is needed
- Full AWS customization is necessary

---

## Typical Stack on Lightsail

Frontend  
Next.js / React

Backend  
Node.js / NestJS

Database  
MySQL / PostgreSQL

Reverse Proxy  
Nginx
