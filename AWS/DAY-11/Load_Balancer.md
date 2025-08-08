## What is a Load Balancer?
A Load Balancer distributes incoming traffic across multiple targets (EC2 instances, containers, or IP addresses) to ensure high availability, fault tolerance, and better performance of applications.

## Types of AWS Load Balancers
AWS provides Elastic Load Balancing (ELB) with four types of load balancers:

Application Load Balancer (ALB)	--> Best for HTTP/HTTPS applications (Layer 7)	HTTP, HTTPS

Network Load Balancer (NLB)	--> Best for low-latency TCP/UDP applications (Layer 4)	TCP, UDP, TLS

Gateway Load Balancer (GWLB) --> Best for deploying security appliances	IP packets

Classic Load Balancer (CLB)	--> Legacy option (supports both Layer 4 & 7 but limited features)	HTTP, HTTPS, TCP, SSL

### Application Load Balancer (ALB) - Layer 7
Works at application layer (Layer 7) of the OSI model.

Routes requests based on content, such as URL paths, HTTP headers, and query strings.

Supports host-based & path-based routing.

Can integrate with AWS Auto Scaling Groups.

Used for microservices, APIs, and containerized applications (ECS, EKS).

✅ Use Case: Websites, APIs, and applications with multiple endpoints (e.g., /login, /cart).

### Network Load Balancer (NLB) - Layer 4
Works at transport layer (Layer 4) of the OSI model.

Routes traffic based on IP & port, without inspecting the request contents.

Ultra-low latency and can handle millions of requests per second.

Supports static IP addresses or Elastic IPs.

Used for high-performance networking applications.

✅ Use Case: Real-time gaming, financial transactions, or high-volume TCP/UDP applications.

### Gateway Load Balancer (GWLB) - Layer 3
Works at network layer (Layer 3).

Routes IP packets to security appliances like firewalls or intrusion detection systems.

Ensures inline security appliance scaling.

✅ Use Case: Deploying virtual firewalls, intrusion prevention systems, and deep packet inspection.

### Classic Load Balancer (CLB) - Legacy
Supports both Layer 4 (TCP/SSL) and Layer 7 (HTTP/HTTPS).

Does not support advanced routing features (like ALB).

Being phased out in favor of ALB and NLB.

✅ Use Case: Legacy applications still using CLB.

## Load Balancer Components
Listeners → Rules that define how incoming traffic is handled (e.g., port 80 for HTTP).
Target Groups → A group of EC2 instances, IPs, or Lambda functions to which traffic is sent.
Health Checks → Checks the health of target instances and removes unhealthy ones automatically.

## Key Features of AWS Load Balancers
Elastic Scaling: Automatically adjusts to handle varying traffic loads.

High Availability & Fault Tolerance: Ensures traffic is always routed to healthy instances.

Security: Works with AWS Shield, WAF (Web Application Firewall), and IAM policies.

Cross-Zone Load Balancing: Distributes traffic evenly across multiple Availability Zones.

SSL/TLS Termination: Encrypts/decrypts traffic to improve performance.

## AWS Load Balancer Pricing
Pricing depends on:
Number of Load Balancer hours used
Number of new connections per second

