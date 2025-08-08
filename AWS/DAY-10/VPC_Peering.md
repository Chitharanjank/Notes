# AWS VPC Peering & IAM Role for SSM Full Access to Connect Private EC2
## 1. AWS VPC Peering
VPC Peering allows two Virtual Private Clouds (VPCs) to communicate privately using AWS' internal network. This is useful when you need to connect resources in different VPCs without exposing them to the internet.

### How VPC Peering Works?
Direct Private Connection: The traffic between the two VPCs stays within AWS’ network, reducing latency and security risks.

No Transitive Peering: If VPC A is peered with VPC B, and VPC B is peered with VPC C, A cannot communicate with C.

Same or Different AWS Accounts: Peering can be done within the same AWS account or across different accounts.

### Steps to Set Up VPC Peering
#### Create a Peering Connection
Go to the AWS VPC Console → Peering Connections → Create Peering Connection.

Choose the VPCs to peer (either within the same account or different accounts).

Select the AWS region (Peering can be inter-region or intra-region).

Accept the Peering Request

If peering with a different account, the owner of the other VPC must accept the request.

#### Update Route Tables
In both VPCs, update route tables to allow traffic to pass between them.

Example: If VPC A has CIDR 10.0.0.0/16 and VPC B has 192.168.0.0/16, add the following:

In VPC A’s route table → Destination 192.168.0.0/16, Target: Peering connection.

In VPC B’s route table → Destination 10.0.0.0/16, Target: Peering connection.

#### Security Groups & NACLs
Ensure security groups and network ACLs allow traffic between the two VPCs.



## 2. IAM Role with SSM Full Access for Private EC2
When an EC2 instance is in a private subnet (without direct internet access), you can use AWS Systems Manager (SSM) Session Manager to connect to it without SSH or bastion hosts.

## How It Works?
AWS Systems Manager Session Manager allows you to connect to an EC2 instance through the AWS console or AWS CLI.
Instead of using SSH, it establishes a connection using the SSM Agent installed on the instance.
The IAM Role attached to the EC2 instance must have SSM Full Access permission.
The EC2 instance must have access to SSM endpoints either through a VPC endpoint or NAT Gateway.

## Steps to Set Up IAM Role for SSM on a Private EC2
### 1. Create an IAM Role for SSM
Go to IAM Console → Roles → Create Role.

Select AWS Service → Choose EC2 as the trusted entity.

Attach the policy AmazonSSMManagedInstanceCore (this gives SSM full access).

Name the role and create it.


### 2. Attach IAM Role to EC2 Instance
Go to EC2 Console → Select your private EC2 instance → Click Actions → Security → Modify IAM Role.
Attach the IAM Role created in Step 1.

### 3. Ensure SSM Agent is Installed on the EC2 Instance
If using Amazon Linux 2 or Ubuntu, the SSM Agent is pre-installed.

If not installed, run:
    
        sudo yum install -y amazon-ssm-agent  # Amazon Linux
        sudo apt install -y amazon-ssm-agent  # Ubuntu/Debian


## 4. Connect to Private EC2 Using Session Manager
Go to EC2 Console → Select the EC2 instance.
Click Connect → Choose Session Manager → Click Start Session.

# EXAMPLE ARCHITECTURE
![My Image](/Images/VPC_PEERING.jpg)