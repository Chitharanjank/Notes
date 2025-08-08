# AWS Backup

A managed service that automates backup tasks for EC2 and other AWS services.
Stores backups in AWS Backup Vault (a centralized location for backup storage).
Supports backup scheduling, retention policies, and encryption.

## How to Enable AWS Backup for EC2?

Go to AWS Backup in the AWS Console.
Create a Backup Plan (choose predefined or custom).
Select EC2 as a resource.
Define backup frequency (e.g., daily, weekly).
Choose a retention period (how long backups are kept).
Store backups in a Backup Vault (default or custom vault).

## AWS Backup Features

Automatic backup scheduling.
Cross-region and cross-account backup options.
Supports backup encryption.
Set lifecycle policies (move older backups to cold storage to reduce costs).

# AWS Trusted Advisor
AWS Trusted Advisor is a service that provides best practices and recommendations to improve security, performance, and cost efficiency.

## What is AWS Trusted Advisor?

A tool that gives recommendations in five key categories:
Cost Optimization – Identify underutilized resources to reduce cost.
Performance – Improve performance by optimizing resources.
Security – Detect security gaps (e.g., public S3 buckets, IAM policies).
Fault Tolerance – Ensure high availability and resilience.
Service Limits – Monitor usage of AWS service limits..