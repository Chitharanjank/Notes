#  Types of Load Balancers in AWS

---

##  What is a Load Balancer?

A Load Balancer automatically distributes incoming traffic across multiple targets (such as EC2 instances, containers, or IPs) to ensure:

- High availability  
- Fault tolerance  
- Scalability  
- Performance

---

##  Types of Load Balancers in AWS

AWS provides **three main types** of Elastic Load Balancers (ELB):

---

### 1. ✅ Application Load Balancer (ALB)
- Operates at **Layer 7** (HTTP/HTTPS)
- Supports:
  - Path-based routing (`/login`, `/images`)
  - Host-based routing (`api.example.com`)
  - WebSocket & HTTP/2
- Best suited for:
  - Web applications
  - Microservices
- Can route to:
  - EC2 instances
  - Lambda functions
  - Containers

---

### 2.  Network Load Balancer (NLB)
- Operates at **Layer 4** (TCP/UDP)
- Extremely fast with ultra-low latency
- Can handle millions of requests per second
- Best suited for:
  - High-performance, real-time applications
  - TCP-heavy workloads
- Supports static IP & Elastic IP

---

### 3.  Gateway Load Balancer (GWLB)
- Operates at **Layer 3/4**
- Combines load balancing with traffic inspection
- Integrates with 3rd-party appliances (like firewalls, intrusion detection)
- Best suited for:
  - Transparent traffic forwarding
  - Security & monitoring

---

##  Comparison Table

| Feature             | ALB                        | NLB                        | GWLB                       |
|---------------------|-----------------------------|-----------------------------|-----------------------------|
| OSI Layer           | 7 (Application)            | 4 (Transport)              | 3/4 (Network)              |
| Protocols           | HTTP, HTTPS, WebSocket     | TCP, UDP, TLS              | All traffic types          |
| Routing Type        | Path/Host/Headers          | Port/Protocol based        | Transparent forwarding     |
| Target Types        | EC2, IP, Lambda            | EC2, IP                    | Security appliances        |
| Best For            | Web apps, APIs             | High-perf TCP apps         | Traffic inspection         |
| Static IP           | ❌ (only via NLB front)     | ✅                         | ✅                         |
| Health Checks       | HTTP/HTTPS                 | TCP                        | TCP/ICMP                   |

---

##  Summary

- **Use ALB** for websites, REST APIs, and app-layer routing.
- **Use NLB** for high-performance TCP/UDP traffic and real-time systems.
- **Use GWLB** for security-related traffic filtering and inspection.

---

💡 Pro Tip: You can use Auto Scaling Groups (ASGs) behind any ELB for better availability & performance.

