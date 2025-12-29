# Introduction to Virtual Private Cloud (VPC)

## What is VPC?

A Virtual Private Cloud (VPC) is a logically isolated network in the cloud where you can launch and manage AWS resources.
It allows you to define IP address ranges, subnets, route tables, and gateways to control traffic flow.
Similar to a traditional data center but in the cloud.

## Key Features of VPC:

Isolation: Your own private cloud environment.

Customizable IP range: You can define your own CIDR block (e.g., 10.0.0.0/16).

Security: Use Security Groups and Network ACLs to control traffic.


## Route Table

What is a Route Table?

A Route Table contains rules (routes) that determine how network traffic is directed within a VPC.
Each subnet in a VPC must be associated with a route table.

### Types of Route Tables:
Main Route Table – Default route table for all subnets unless explicitly changed.

Custom Route Table – You can create additional route tables for specific subnets.

## Internet Gateway (IGW)

What is an Internet Gateway?
An Internet Gateway (IGW) is a component that allows resources in a public subnet to communicate with the internet.
It provides NAT (Network Address Translation) for outgoing traffic and enables incoming traffic to reach resources with a public IP.

### How IGW Works?
Attach IGW to VPC – It must be explicitly attached to a VPC.

Route Table Configuration – The public subnet's route table should have a route like:

```Destination: 0.0.0.0/0 → Target: igw-xxxxx```

Assign Public IP – Instances must have a public IPv4 address or an Elastic IP.

## Public Subnet

What is a Public Subnet?
A Public Subnet is a subnet where resources can access and be accessed from the internet.
It is connected to an Internet Gateway (IGW).

### EC2 instances in a public subnet must have:
A public IP

A route to the Internet Gateway (IGW)

### How to Make a Subnet Public?
Attach an IGW to the VPC.

Modify the route table associated with the subnet:

```Destination: 0.0.0.0/0 → Target: igw-xxxxx```

Ensure the EC2 instance has a Public IP.


## Dynamic Public IP (Auto-assigned Public IP)

What is a Dynamic Public IP?
A temporary public IP assigned to an instance at launch.
Assigned automatically when an instance is created if enabled.

### Changes when:
The instance is stopped and started.

The instance is terminated and relaunched.

### Use Case:
When public access is required but permanent IP is not needed.

Suitable for temporary or short-lived workloads.


## Elastic IP (EIP)

What is an Elastic IP?
A static, fixed public IP that you can manually assign to an instance.
Remains permanently associated with your AWS account until manually released.
Can be reassigned to another instance if needed.

### Does NOT change when:
The instance is stopped and started.

The instance fails and needs to be restarted.

### Important Notes About Elastic IPs:
AWS provides one Elastic IP for free, but only if it’s associated with a running instance., If not associated, AWS charges you for keeping it idle.
You can only have a limited number of Elastic IPs per AWS account (default limit is 5 per region, but you can request an increase).

### Use Case:
When a permanent public IP is needed, such as:

Hosting a website.

Running a production service that requires a fixed IP.

Configuring a NAT Gateway to allow private instances to access the internet.

## Architecture & Rough Notes

![My Image](Images/VPC-DAY-1.png)
