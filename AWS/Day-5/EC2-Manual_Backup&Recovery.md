# AWS Manual Backup and Recovery (EC2 AMI) Notes

## 1. What is an AMI?
AMI (Amazon Machine Image) is a pre-configured template that contains the OS, application server, and applications.
Used to launch new EC2 instances with the same configuration.

## 2. Why Backup EC2?
Protects data from accidental deletion, corruption, or system failures.
Allows easy restoration of instances in case of issues.

## 3. Steps to Create a Manual Backup (AMI of an EC2 Instance)
Log in to AWS Console → Open EC2 Dashboard.

Select the Instance → Choose the EC2 instance you want to back up.

### Create Image (AMI):
Click Actions → Image and templates → Create Image.

Enter Image Name and optional description.

Choose No reboot (optional) if you don’t want downtime.

Create AMI → Click Create Image.

### Verify the AMI:
Navigate to Images → AMIs and check if the status is "Available".

## 4. Restoring from AMI (Recovery Process)
Go to AMIs → Select the required AMI.

### Launch Instance from AMI:

Click Launch Instance from Image.

Choose instance type, configure settings, and click Launch.

Attach Elastic IP (if required) and update security groups.

Verify the instance is working properly.

## 5. Important Considerations

AMIs are region-specific; copy them to another region if needed.

Store AMIs in Amazon S3 (as part of snapshots).

Delete old AMIs to reduce storage costs..