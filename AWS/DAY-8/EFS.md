# AWS EFS (Elastic File System)
AWS Elastic File System (EFS) is a fully managed, scalable, and serverless file storage service for use with AWS EC2, Lambda, and on-premises servers.

## What is AWS EFS?
A managed NFS (Network File System) that provides shared file storage for multiple EC2 instances.
Auto-scaling – Grows and shrinks as you add or remove files.
Pay-as-you-use pricing model – No need to provision storage in advance.
Supports Linux-based workloads (not Windows).

## Key Features
Scalability – Automatically scales up/down without user intervention.

High Availability & Durability – Data is stored across multiple AZs in a region.

Multiple EC2 Access – Can be mounted on multiple EC2 instances simultaneously.

## Performance Modes:
General Purpose (default) – Balanced for most workloads.

Max I/O – Best for high-throughput workloads.

## Storage Classes:
Standard – Regular, high-performance storage.

Infrequent Access (IA) – Cheaper, for less frequently accessed data.

Basic Steps to Use EFS:

## Create an EFS File System
Go to AWS Console → EFS → Create a new file system.

Choose VPC 

Mount EFS on EC2 Instance

### Install NFS client
      sudo yum install -y amazon-efs-utils  # (For Amazon Linux)

      sudo apt install -y nfs-common         # (For Ubuntu)

## Create a mount directory

      sudo mkdir /mnt/efs

## Mount EFS
      sudo mount -t efs fs-xxxxxx:/ /mnt/efs

## Verify by running:

     df -h