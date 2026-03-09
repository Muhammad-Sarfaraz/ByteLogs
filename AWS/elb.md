# Elastic Load Balancing (ELB)


## Overview
Elastic Load Balancer (ELB) is an AWS service that distributes incoming traffic across multiple servers (EC2 instances) automatically.  
Purpose:
- Improve availability
- Prevent server overload
- Enable horizontal scaling

Flow:
User Request -> Load Balancer -> Multiple Servers

---

## Types of ELB

### 1. Application Load Balancer (ALB)
- Layer: Layer 7 (HTTP/HTTPS)
- Best for: Web apps, microservices, containers
- Features:
  - Path-based routing
  - Host-based routing
  - WebSocket support
- Example:
api.example.com -> API service
app.example.com -> Frontend service

Or:
 /api -> backend server
 / -> frontend server

### 2. Network Load Balancer (NLB)
- Layer: Layer 4 (TCP/UDP)
- Best for: High performance, low latency
- Features:
  - Static IP
  - Handles sudden traffic spikes
- Use cases: Gaming servers, real-time systems, financial systems

### 3. Gateway Load Balancer (GWLB)
- Use for: Security appliances, firewalls, network inspection
- Less common for standard web apps

---

## How ELB Works
Users
   |
   v
Load Balancer
   |
  +---+---+---+
  |   |   |   |
Server1 Server2 Server3

- Distributes requests evenly
- If a server fails, traffic automatically goes to healthy servers

---

## Key Features

### Health Checks
- ELB continuously checks server health
- Example: GET /health
- Failing servers are removed from traffic

### SSL Termination
- ELB handles HTTPS encryption
User -> HTTPS -> ELB -> HTTP -> Backend
- Reduces CPU load on servers
- Centralized certificate management

### Auto Scaling Integration
- Works with Auto Scaling Groups
- Example:
High traffic -> new servers start
Low traffic -> servers stop

---

## Example Production Architecture
Users
   |
   v
Route53 (DNS)
   |
   v
Application Load Balancer
   |
   v
EC2 Instances (App Servers)
   |
   v
Database

---

## Advantages
- High availability
- Automatic traffic distribution
- Fault tolerance
- SSL management
- Scales automatically

---

## Common Use Cases
- High traffic websites
- SaaS applications
- Microservice architectures
- API gateways
- Container platforms

---

| Scaling | Limited      | Highly scalable |
| Routing | Basic        | Advanced routing |
| Use Case| Small apps   | Production systems |
