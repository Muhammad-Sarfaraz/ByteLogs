# EC2

EC2 Storage Increase

To expand the root partition after increasing the EC2 volume size:

```sh
# Check current disk usage
df -h

# Extend the partition to use the new space
sudo growpart /dev/xvda 1

# Resize the filesystem
sudo resize2fs /dev/xvda1

# Verify the updated disk usage
df -h
```

## EC2 Instance Metadata Service (169.254.169.254)

## Overview
Cloud providers expose a special internal endpoint that allows a virtual machine to retrieve information about itself.  

In **Amazon EC2**, this endpoint is:

```
169.254.169.254
```

This address belongs to the **link-local IP range** and is only reachable from inside the instance. It is **not accessible from the internet** and does not belong to any public organization.

When a request is sent to this IP, the **AWS hypervisor intercepts it** and routes it to the **Instance Metadata Service (IMDS)**.

Provider: **Amazon Web Services (AWS)**  
Service: **EC2 Instance Metadata Service (IMDS)**

---

# Purpose

The metadata service allows applications running inside the EC2 instance to dynamically discover configuration information about the environment **without hardcoding values**.

Typical examples include:

- Instance type detection
- Instance ID retrieval
- Region / availability zone discovery
- IAM temporary credentials
- Networking information
- Startup scripts

---

# Example Metadata Queries

## Instance Type

```bash
curl http://169.254.169.254/latest/meta-data/instance-type
```

## Instance ID

```bash
curl http://169.254.169.254/latest/meta-data/instance-id
```

## Private IP

```bash
curl http://169.254.169.254/latest/meta-data/local-ipv4
```

## Public IP

```bash
curl http://169.254.169.254/latest/meta-data/public-ipv4
```

## Availability Zone

```bash
curl http://169.254.169.254/latest/meta-data/placement/availability-zone
```

## IAM Role Credentials

```bash
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/
```

## User Data Script

```bash
curl http://169.254.169.254/latest/user-data
```

---

# Security Consideration

Although the metadata endpoint is **local**, it contains **sensitive information**.

If a web application has a **Server-Side Request Forgery (SSRF)** vulnerability, an attacker may force the server to request:

```
169.254.169.254
```

This could expose:

- IAM temporary credentials
- instance configuration
- network details

To mitigate this risk, **AWS introduced IMDSv2**, which requires a **session token** before accessing metadata.

---

# Interesting Fact

Most major cloud providers use the **same metadata IP address**:

| Cloud Provider | Metadata IP |
|----------------|-------------|
| AWS EC2 | 169.254.169.254 |
| Google Cloud | 169.254.169.254 |
| Microsoft Azure | 169.254.169.254 |

Even though the IP is the same, the **metadata structure and authentication systems differ** between providers.

---

# Key Takeaway

`169.254.169.254` is a **special internal endpoint provided by cloud infrastructure** that allows instances to retrieve metadata about themselves.

It is extremely useful for automation but should always be treated as a **sensitive resource** and protected against **SSRF attacks**.
