# 📘 AWS DynamoDB and Lambda Notes for Beginners

---

## 📦 What is AWS DynamoDB?

**DynamoDB** is a **NoSQL** database service provided by AWS.

- Fully managed, serverless
- Key-Value and Document store
- High performance and scalable
- Built-in **auto-scaling** and **backup**

---

##  Example Table

Imagine a table called `Users`:

| user_id (PK) | name    | email               |
|--------------|---------|---------------------|
| 101          | Alice   | alice@email.com     |
| 102          | Bob     | bob@email.com       |

---

## ✅ Use Cases

- User profiles
- Sensor/IoT data
- Real-time apps (chat, gaming)
- Serverless web apps

---

##  DynamoDB Features

- Auto-scaling read/write capacity
- On-demand or provisioned capacity
- Streams (for triggers)
- TTL (Time To Live) for auto-deleting data
- Encryption (KMS)
- Backup & restore

---

##  How to Create a DynamoDB Table

1. Go to **AWS Console**
2. Search **DynamoDB**
3. Click **Create table**
4. Set:
   - Table name: `Users`
   - Partition key: `user_id`
5. Leave other defaults and click **Create**

---

#  AWS Lambda

---

##  What is AWS Lambda?

AWS Lambda is a **serverless compute service** provided by AWS.

> You write the code. AWS runs it **automatically** in response to **events** like HTTP requests, file uploads, or database updates.

---

## ✅ Key Features

- **Serverless** – no server setup needed
- **Event-driven** – runs code in response to triggers (S3, API Gateway, etc.)
- **Auto Scaling** – scales based on requests
- **Supports many languages** – Python, Node.js, Java, Go, etc.
- **Pay-per-use** – only pay for time and memory used

---

##  Lambda Use Cases

- REST APIs (with API Gateway)
- Scheduled jobs (cron)
- Image/video processing (via S3 triggers)
- Real-time stream processing (via DynamoDB/Kinesis)

---

##  Creating a Lambda Function (Console)

1. Go to **AWS Lambda Console**
2. Click **Create function**
3. Choose:
   - **Author from scratch**
   - Function name (e.g., (e.g., `HelloLambda`)
   - Runtime (e.g., Python 3.9)
4. Click **Create function**
5. Add your code and click **Deploy**
6. Use **Test** to run it manually

---

##  Sample Python Lambda Function

```python
def lambda_handler(event, context):
    print("Received event:", event)
    return {
        'statusCode': 200,
        'body': 'Hello from Lambda!'
    }
