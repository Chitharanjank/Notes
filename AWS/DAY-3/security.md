## 1. Vertical Scaling
Vertical scaling (also known as scaling up/down) refers to increasing or decreasing the compute capacity of a single server by upgrading its resources, such as:

CPU (e.g., upgrading from 2 cores to 8 cores)
RAM (e.g., increasing memory from 4GB to 32GB)
Storage (e.g., upgrading disk space)

### Advantages
✅ Simple and easy to implement
✅ No need to modify applications
✅ Suitable for applications that cannot be distributed

### Disadvantages
❌ Hardware limitations (can scale only up to a certain point)
❌ Downtime may be required while upgrading
❌ More expensive as resources increase

## 2. User Data (AWS EC2 User Data)
User Data in AWS EC2 allows running scripts automatically when an instance first launches. This is typically used for:

### Installing software packages
### Configuring the server
### Running initialization scripts

## How it Works?
User Data scripts run only once during the first boot
It supports shell scripts (#!/bin/bash) and cloud-init scripts

Example: (A script to install Apache on an EC2 instance)
```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "hello world" > /var/www/html/index.html
```
## 3. Security Groups (SG) in AWS
Security Groups act as virtual firewalls for EC2 instances, controlling inbound and outbound traffic at the instance level.

### Key Features:
Works at the instance level (attached to EC2)
Supports allow rules only (no deny rules)
By default, all inbound traffic is denied and all outbound traffic is allowed

## 4. Network ACL (NACL) in AWS
Network ACLs (NACLs) are firewalls at the subnet level, controlling traffic in and out of subnets.

### Key Features:
Works at the subnet level
Supports both allow and deny rules
Evaluates rules in order (starting from the lowest numbered rule)

## Architecture

![My Image](/Images/Security.jpg)








