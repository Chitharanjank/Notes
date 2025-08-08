# AWS NAT Gateway, Elastic IP, and Jump Server

## 1️⃣ NAT Gateway (Network Address Translation Gateway)
📌 What is a NAT Gateway?
NAT Gateway allows instances in a private subnet to access the internet without exposing them to the public.
It enables outbound internet access but blocks inbound connections from the internet.

### 🛠️ How It Works?
Private EC2 instances send requests to the internet (e.g., yum install httpd).
The NAT Gateway receives this traffic and replaces the private IP with its Elastic IP (EIP).
The response from the internet is sent back to the NAT Gateway, which forwards it to the private EC2.

### ✅ Key Features
Requires an Elastic IP (EIP) to function.
Placed in a public subnet.
Supports only outbound connections.
Highly available in a single Availability Zone.

### 📌 Why Use NAT Gateway?
Private instances cannot directly access the internet (no public IP).
NAT Gateway acts as a middleman for secure internet access.
Used for downloading updates, patches, and installing software in private instances.

## 2️⃣ Elastic IP (EIP)
📌 What is an Elastic IP?
A static, public IPv4 address provided by AWS.
It remains the same even if the instance is stopped and restarted.
Used for NAT Gateway, Bastion Hosts (Jump Servers), and critical applications that require a fixed IP.

### ✅ Key Features
One Elastic IP is free if attached to a running instance.
AWS charges if an EIP is allocated but not in use.
Can be reassigned to another instance in case of failure.

### 📌 Why Use Elastic IP?
Ensures consistent public access (for Bastion Host, NAT, or web servers).
Provides failover capability in case of instance failure.
Helps in whitelisting static IPs in firewall rules.

## 3️⃣ Jump Server (Bastion Host)
📌 What is a Jump Server?
A publicly accessible EC2 instance that acts as an intermediary to connect to private instances.
Used to secure SSH access to private servers without exposing them to the internet.

### 🛠️ How It Works?
You connect to the Jump Server using SSH (ssh ec2-user@jumpserver-public-ip).
From the Jump Server, you connect to private instances (ssh private-ec2-user@private-ip).

### ✅ Key Features
Hardened security: Limited access, only allows SSH connections.
Acts as a single entry point for accessing private instances.
Configured with security groups to restrict access (e.g., only allow SSH from trusted IPs).

### 📌 Why Use a Jump Server?
Prevents direct internet exposure of private instances.
Improves security by limiting SSH access to a single, controlled instance.
Easier management of private instances.

## Architecture

![My Image](/Images/NAT.jpg)
