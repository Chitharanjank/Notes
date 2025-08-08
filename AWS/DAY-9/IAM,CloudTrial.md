# AWS IAM (Identity and Access Management)
IAM is a web service that helps you securely control access to AWS resources.
It enables users, groups, roles, and policies to define who can access what in AWS.
IAM is global and does not require a specific region.

## IAM Components
### (A) IAM Users
A user represents an individual with long-term access credentials (username, password, access keys).
Users can be assigned permissions using policies.
By default, a new IAM user has no permissions.


### (B) IAM Groups
A group is a collection of IAM users.
Instead of assigning policies to individual users, attach policies to groups.

#### Example:
Developers Group → Full access to EC2

Support Group → Read-only access to S3


### (C) IAM Policies
Policies are JSON documents that define what actions are allowed or denied for users, groups, and roles.
Policies follow the AWS Policy Language with Effect, Action, Resource, Condition.

#### Example JSON policy:

            {
              "Version": "2012-10-17",
              "Statement": [
                {
                  "Effect": "Allow",
                  "Action": "s3:ListBucket",
                  "Resource": "arn:aws:s3:::example-bucket"
                }
              ]
            }

#### Types of Policies:
AWS Managed Policies: Predefined by AWS.

Customer Managed Policies: Created by users.

Inline Policies: Attached directly to a user, group, or role.


### (D) Multi-Factor Authentication (MFA)
Adds an extra layer of security (password + one-time code).
Recommended for:
Root account (mandatory for better security).
IAM users with console access.


### (E) IAM Roles
IAM Roles are temporary credentials assigned to AWS services, users, or applications.
Use cases:
EC2 instance roles (allow EC2 to access S3, DynamoDB, etc.).
Cross-account access (one AWS account grants access to another).
Lambda function roles (allow Lambda to interact with AWS services).



# AWS CloudTrail
CloudTrail logs all API calls made in an AWS account.
Used for auditing, security monitoring, and troubleshooting.
By default, CloudTrail logs the last 90 days of events.
To store logs permanently, enable logging to S3.
