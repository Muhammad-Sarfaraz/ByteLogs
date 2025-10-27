# Networking

#### Client-Server



#### Sockets, 

#### DNS, 

#### TCP/IP, 

#### Web Server, 

#### Ping, 

#### Traceroute, 

#### Web Server, 

#### Routing, 

#### Top-Down Layered Model.

### 3. Gateway / NAT

The company has a gateway/router that connects the private network to the internet.

The gateway has:

- One interface in the private subnet (`192.168.1.1`)
- One interface with the public IP (`203.0.113.10`)

**When you browse the internet:**

1. Your PC sends a packet to, e.g., `8.8.8.8`.
2. Packet goes to the **gateway**.
3. Gateway does **NAT (Network Address Translation)**:
   - Rewrites source IP: `192.168.1.10` → `203.0.113.10`
4. Internet sees the request coming from `203.0.113.10`.
5. Gateway rewrites the response back to your **private IP**.

```

        Private Subnet (192.168.1.0/24)
        -------------------------------
        |                             |
 [PC1:192.168.1.10]           [PC2:192.168.1.11]
        |                             |
        +-------------+---------------+
                      |
                      v
             +-------------------+
             |  Company Gateway  |
             |------------------|
             | Private IP:       |
             | 192.168.1.1       |
             | Public IP:        |
             | 203.0.113.10      |
             +-------------------+
                      |
                      v
                   Internet
                      |
                      v
                 [DNS: 8.8.8.8]
```


