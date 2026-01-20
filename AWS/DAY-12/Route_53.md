
# Domain Name (GoDaddy)
A domain name is a human-readable address (e.g., www.example.com) that maps to an IP address.
GoDaddy is a domain registrar where you purchase and manage domain names.

# Route 53 (AWS DNS Service)
Amazon Route 53 is a Domain Name System (DNS) service that translates domain names to IP addresses.
It directs traffic to AWS resources like Load Balancers, EC2 instances, or S3 buckets.
Route 53 works like a phone directory – when you type a domain, it finds the corresponding IP.

# Elastic Load Balancer (ELB)
AWS Elastic Load Balancer (ALB, NLB, CLB) distributes incoming requests across multiple servers (EC2 instances).
In this project, we use an Application Load Balancer (ALB) to handle traffic efficiently.

# Virtual Private Cloud (VPC) & Subnets
A VPC (Virtual Private Cloud) is like your private AWS data center.
It consists of subnets (public and private):
Public Subnets: Host internet-facing services like Load Balancers.
Private Subnets: Host backend services (e.g., Home, Catalog, Payment microservices).

# How Traffic Flows from Browser to Server
When a user types www.example.com in their browser, here’s how traffic flows step by step:                                                                                            
## Step 1: User Enters Domain in Browser
The browser sends a DNS query to resolve www.example.com to an IP address.

## Step 2: GoDaddy & Route 53 Handle the Request
GoDaddy (where you registered the domain) has Name Server (NS) records pointing to Route 53.
Route 53 receives the request and checks its DNS records to find where to send the traffic.

## Step 3: Route 53 Resolves to Load Balancer
Route 53 checks its A record (Alias Record) or CNAME Record and returns the Load Balancer’s DNS name (e.g., example-alb-1234.amazonaws.com).
The browser now knows where to send the request.

## Step 4: Load Balancer Receives Traffic
The browser makes an HTTP request to the ALB.
The ALB is in the public subnet and accepts incoming requests.

## Step 5: ALB Routes Request to Target Groups
The ALB checks routing rules (Host-based or Path-based):
/home → TG-01 (Home Page)
/catalog → TG-02 (Catalog Service)
/payment → TG-03 (Payment Service)

## Step 6: Traffic Reaches Private Subnet & EC2 Instances
The request is forwarded to the corresponding EC2 instance in the private subnet.
The EC2 instance processes the request and sends back the response.

## Step 7: Response Goes Back to User
The EC2 instance returns data to the Load Balancer.
ALB forwards the response back to the browser.
The user sees the webpage loaded successfully.

# Detailed Traffic Flow with Diagram Reference
🛠 From Browser to Server

User enters www.example.com → Browser asks DNS for the IP

GoDaddy’s Name Servers forward the request to Route 53

Route 53 checks DNS records and returns Load Balancer’s DNS

Browser sends request to ALB (Public Subnet)

ALB routes request to the correct Target Group

Target Group forwards request to Private Subnet EC2 instances

EC2 instance processes request & sends response

Response flows back through ALB to User’s Browser

# Architecture
 ![My Image](../Images/Route53.jpg)
