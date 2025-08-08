
# AWS CloudTrail 
## 1. What is AWS CloudTrail?
AWS CloudTrail is a service that enables logging, monitoring, and tracking of API calls and user activities in an AWS account.

Helps with security analysis, compliance auditing, and operational troubleshooting.

## 2. Key Features
Records API Calls: Logs all AWS Management Console, SDKs, CLI, and AWS services API requests.

Event History: Stores the last 90 days of events for free.

Trails for Deeper Logging: Can be configured to send logs to S3 & CloudWatch Logs for long-term storage and analysis.

Multi-Region & Multi-Account Tracking: Can enable logging across all AWS regions.

---

## 3. Types of Events Logged by CloudTrail

### A. Management Events
Actions related to account configuration and resource changes.

Examples:

IAM role creation

EC2 instance start/stop

Security Group modifications

### B. Data Events
Tracks data-level interactions in AWS services like S3, Lambda, and DynamoDB.

Examples:

S3 Object Access (Read, Write)

Lambda Function Invocation

### C. Insights Events
Detects unusual activities like:

A sudden increase in API calls.

Unusual access patterns.

## 4. CloudTrail Components
### A. Event History
Shows last 90 days of API activities.

Cannot be modified or disabled.

### B. Trails
Continuous logging of events beyond 90 days.

Stores logs in Amazon S3, can send them to CloudWatch Logs.


### C. CloudTrail Insights
Detects anomalies in API usage.

Example: Unusual number of failed login attempts.

## 5. CloudTrail vs CloudWatch
| Feature |            CloudTrail	                           |                          CloudWatch                          |   
|---------|----------------------------------------------------|--------------------------------------------------------------|
| Purpose |  Tracks API calls (who did what, where, when)	   |  Monitors metrics, logs, and events for performance & health |
|Data Type|     API activity logs	                           |  Performance logs, custom metrics, and alarms                |
|Retention| 90 days (Event History), unlimited if stored in S3 |  Varies based on log group retention settings                |
|Use Case |    Security auditing & compliance	               |  Real-time monitoring, alerting, troubleshooting             |
