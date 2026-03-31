# AWS Certificate Manager (ACM) 

## 1. Design Intent

AWS Certificate Manager (ACM) is not a general-purpose certificate store. It is an infrastructure-integrated certificate orchestration system designed to:

- Eliminate certificate lifecycle management from application teams  
- Enforce TLS termination at controlled ingress points  
- Prevent private key exposure in customer-managed compute environments  

This is a deliberate architectural constraint, not a limitation.

---

## 2. Core Principle

ACM certificates are attachable, not deployable.

You do not install them.  
You bind them to AWS-managed entry points that perform TLS termination.

Separation of concerns:

| Layer | Responsibility |
|------|----------------|
| Edge (ALB/CloudFront) | TLS termination |
| Compute (EC2/ECS/EKS) | Application logic |

---

## 3. Architectural Model

### 3.1 TLS Termination Strategy

Client → TLS → Edge (ALB / CloudFront) → HTTP → Backend

Rationale:
- Reduces cryptographic overhead on compute  
- Standardizes TLS policy enforcement  
- Enables observability and security controls at ingress  

---

### 3.2 Trust Boundary Placement

The trust boundary ends at the load balancer or edge network.

Implications:
- Traffic inside VPC is assumed trusted (unless mTLS is implemented)  
- Encryption-in-transit inside VPC is optional  

---

## 4. Integration Constraints

ACM integrates only with:

- Elastic Load Balancing (ALB / NLB)  
- Amazon CloudFront  
- API Gateway  
- App Runner  

It does NOT support:
- Direct EC2 attachment  
- Arbitrary certificate export  

Reason:
- Prevents key exfiltration  
- Ensures TLS termination in AWS-controlled environments  

---

## 5. Certificate Lifecycle

### Issuance
- Public certificates issued via Amazon Trust Services  
- Requires domain validation  

### Validation

DNS Validation (Recommended):
- Add CNAME record to DNS  
- Enables automatic renewal  

Email Validation:
- Manual approval  
- Not suitable for production  

---

### Renewal
- Fully automatic  
- Requires:
  - Certificate in use  
  - DNS record intact  

Failure mode:
- Removing DNS record breaks renewal silently  

---

## 6. Regional and Global Rules

Regional (ALB / NLB):
- Certificate must be in the same region  

Global (CloudFront):
- Certificate must be in us-east-1  

---

## 7. Security Model

### Key Management
- Private keys are non-exportable  
- Stored in AWS-managed secure systems  

### TLS Policy
- Controlled at ALB / CloudFront  
- Defines TLS versions and cipher suites  

### IAM Control
- Permissions for requesting and attaching certificates  

---

## 8. Performance Considerations

- TLS handled at edge  
- Backend load reduced  
- HTTP/2 supported  
- Lower latency with CloudFront  

---

## 9. Certificate Design Strategies

### Wildcard
*.example.com

Pros:
- Easy scaling  

Cons:
- Larger blast radius  

---

### SAN (Multi-domain)
example.com  
api.example.com  
admin.example.com  

Pros:
- Explicit control  

Cons:
- Requires updates  

---

### Strategy

- Use wildcard for dynamic systems  
- Use SAN for controlled domains  
- Avoid mixing unrelated domains  

---

## 10. Failure Modes

- DNS record removed → renewal fails  
- Wrong region → cannot attach  
- Using ACM in EC2 → unsupported  

---

## 11. Cost Model

- Public certificates: Free  
- Private CA: Paid  
- ALB / CloudFront: Paid  

---

## 12. When NOT to Use ACM

Avoid if:
- You need TLS inside EC2  
- You need certificate export  
- You need full key control  

Use:
- Let’s Encrypt (acme.sh)  
- Custom PKI  

---

## 13. Recommended Architectures

Standard:
Route53 → ALB → EC2  

Edge:
CloudFront → ALB → Backend  

Internal:
Private CA → Internal LB → Services  

---

## 14. Mental Model

ACM is not about certificates.

It is about:
- Secure ingress  
- Managed TLS  
- Removing responsibility from application layer  

---
