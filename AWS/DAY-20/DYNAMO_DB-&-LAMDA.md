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



## 1) Create SNS topic and subscribe your email (Console)

1. Console → **SNS** → **Topics** → **Create topic** → **Standard**.

   * Name: `my-s3-notify-topic` → Create topic.
2. Open the topic → **Create subscription** → Protocol: **Email** → Endpoint: `you@youremail.com` → Create subscription.
3. **IMPORTANT:** Open your email and **click the Confirm subscription** link in the SNS email. (SNS will not deliver until confirmed.)

---

## 2) Create the Lambda execution role (Console, least privilege)

1. Console → **IAM** → **Roles** → **Create role**.
2. Choose **AWS service** → **Lambda** → Next.
3. Attach managed policy **AWSLambdaBasicExecutionRole** (this allows CloudWatch logging). Create role (name: `lambda-s3-sns-role`).
---

## 3) Create the S3 bucket (Console) 

1. Console → **S3** → **Create bucket**.
2. Bucket name: `my-demo-s3-bucket` (must be globally unique) → Region: same region as Lambda and SNS → Create.
   (Leave public access blocked unless you need otherwise.)

---

## 4) Create the Lambda function (Console)

1. Console → **Lambda** → **Create function** → **Author from scratch**.

   * Name: `my-s3-notify-lambda`
   * Runtime: **Python 3.11** (or 3.10)
   * Permissions: **Use an existing role** → choose `lambda-s3-sns-role` → Create function.

2. In the function page: **Configuration → Environment variables** → Add:

   * `SNS_TOPIC_ARN` = `arn:aws:sns:REGION:ACCOUNT_ID:MY_TOPIC_NAME`

3. In the code editor (default `lambda_function.py`) paste the code below and **Deploy**.

**Lambda code (copy/paste):**

```python
import boto3
import os
import urllib.parse
import json

s3 = boto3.client('s3')
sns = boto3.client('sns')

def lambda_handler(event, context):
    print("Received event:", json.dumps(event))
    topic_arn = os.environ.get('SNS_TOPIC_ARN')
    if not topic_arn:
        print("SNS_TOPIC_ARN not set; exiting")
        return {"statusCode":400, "body":"SNS_TOPIC_ARN not configured"}

    records = event.get('Records', [])
    for rec in records:
        try:
            s3info = rec['s3']
            bucket = s3info['bucket']['name']
            key = urllib.parse.unquote_plus(s3info['object']['key'])
        except Exception as e:
            print("Skipping record; malformed:", e)
            continue

        # Get metadata (Content-Type, size)
        try:
            head = s3.head_object(Bucket=bucket, Key=key)
            content_type = head.get('ContentType', 'unknown')
            size = head.get('ContentLength', 'unknown')
        except Exception as e:
            print(f"head_object failed for {bucket}/{key}: {e}")
            content_type = "unknown"
            size = "unknown"

        message = (
            f"New S3 object uploaded\n"
            f"Bucket: {bucket}\n"
            f"Key: {key}\n"
            f"Content-Type: {content_type}\n"
            f"Size: {size} bytes"
        )
        print("Prepared message:\n", message)

        # Publish to SNS
        try:
            resp = sns.publish(TopicArn=topic_arn, Subject="S3 object uploaded", Message=message)
            print("SNS publish response:", resp)
        except Exception as e:
            print("Error publishing to SNS:", e)

    return {"statusCode": 200, "body": "done"}
```


* It reads the S3 event records, does `head_object` to fetch `Content-Type` and size, formats a readable message, and publishes to SNS. All important info goes to the email.

---

## 5) Add S3 trigger to Lambda (Console)

1. In the Lambda function page → **Add trigger**.
2. Choose **S3** → Select your bucket `my-demo-s3-bucket`.
3. Event type: **All object create events** (or choose `PUT` specifically). Optionally set prefix/suffix filters.
4. Add → Save.

> The console will add the necessary resource permission so S3 can invoke your Lambda. If you ever set up notifications directly in S3 (not via the Lambda UI), you may need `aws lambda add-permission` — but using the Lambda console avoids that.

---

## 6) Upload an object using AWS CLI (your requested CLI step)

Make sure your AWS CLI is configured with the same Region and credentials: `aws configure`.

From your terminal:

```bash
# example: upload a local file into the bucket
aws s3 cp ./test-file.txt s3://my-demo-s3-bucket/uploads/test-file.txt --region REGION
```

* This `PutObject` will trigger the S3 event and invoke Lambda.

---

---

## 8) Troubleshooting (common failures)

* **No email** → Check SNS subscription confirmation; check spam folder.
* **Lambda not triggered** → Confirm S3 trigger added to the Lambda (Lambda console → Configuration → Triggers). Make sure bucket and Lambda are in the same region.
* **AccessDenied on `head_object`** → Confirm role inline policy contains `s3:GetObject` for `arn:aws:s3:::MY_BUCKET/*` and `s3:ListBucket` for `arn:aws:s3:::MY_BUCKET`. Also ensure the Lambda role is attached to the function.
* **No logs** → Ensure role has `AWSLambdaBasicExecutionRole` and the function actually executed (check Monitoring → Invocations).
* **Malformed key (spaces, + signs)** → Code uses `urllib.parse.unquote_plus` to decode keys.

---

