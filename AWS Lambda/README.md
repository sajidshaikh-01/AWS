# AWS Lambda – Complete README

Topics Covered:

* What is AWS Lambda
* Lambda Limits
* Passing Data with Event Object
* Lambda Function URLs
* Events in Lambda & Passing Values
* Hot Start vs Cold Start
* Environment Variables
* General Configuration Settings
* Context Object
* Synchronous vs Asynchronous Invocations
* Dead Letter Queue (DLQ)
* Lambda Trigger from S3
* Lambda Trigger from ALB
* External Libraries in Lambda
* Lambda Layers
* Sharing Custom Libraries
* Lambda Versions
* Lambda Aliases
* Resource Policy vs IAM Role
* Lambda in VPC
* Connecting Lambda to RDS
* Reserved Concurrency & Provisioned Concurrency
* Lambda Destinations
* Interview Questions & Answers

---

# 1. What is AWS Lambda?

AWS Lambda is a **serverless compute service** where you run code without provisioning or managing servers. You only pay for compute time used.

Key Features:

* Auto-scaling
* Pay-per-use
* Integrates with 200+ AWS services
* Works with event-driven architectures

---

# 2. AWS Lambda Limits

### **Timeout**: Max 15 minutes

### **Memory**: 128 MB to 10 GB

### **Ephemeral Storage (/tmp)**: Default 512 MB, expandable to 10 GB

### **Package Size**:

* Compressed: 50 MB
* Uncompressed: 250 MB (including layers)

### **Execution Payload Size**:

* Synchronous: 6 MB
* Asynchronous: 256 KB

### **Concurrent Executions**:

* Default account-wide: 1,000 (can request increase)

---

# 3. Passing Data to Lambda (Event Object)

When Lambda is invoked, **event object** carries input data.

Example event:

```json
{
  "name": "sajid",
  "age": 23
}
```

Python access:

```python
def lambda_handler(event, context):
    print(event["name"])
```

---

# 4. Lambda Function URLs (How to Create & Test)

Function URLs provide a **public HTTPS endpoint** for your Lambda.

### Steps:

1. Open Lambda function
2. Go to **Function URL** tab
3. Enable Function URL
4. Choose Auth type (NONE or IAM)

Test via curl:

```bash
curl https://abc123.lambda-url.aws-region.on.aws
```

---

# 5. Events in Lambda – How to Pass Values

Lambda can be triggered from:

* API Gateway
* S3
* DynamoDB Stream
* EventBridge
* SNS
* SQS
* ALB

Each event has a **different structure**.

Example SQS event:

```json
{
  "Records": [
    {
      "body": "Hello World"
    }
  ]
}
```

---

# 6. Lambda Hot Start vs Cold Start

### **Cold Start:**

Occurs when Lambda needs to create a new execution environment.

* Slower
* Happens after inactivity or scaling up

### **Hot Start:**

Uses **already initialized environment**.

* Fast response
* No initialization overhead

### Reduce Cold Starts:

* Use **Provisioned Concurrency**
* Keep package size small
* Use lighter runtimes (Node, Python)

---

# 7. Environment Variables

Used to store config values like DB credentials, API keys.

Python example:

```python
import os
db_name = os.environ['DB_NAME']
```

Stored securely using **KMS encryption**.

---

# 8. General Configuration Settings

Key Lambda configuration items:

* Memory
* Timeout
* IAM Role
* VPC settings
* Environment variables
* Layers
* Runtime
* Architecture (x86_64 / arm64)

---

# 9. Context Object in Lambda

Provides metadata about the invocation.

Python example:

```python
def lambda_handler(event, context):
    print(context.function_name)
    print(context.aws_request_id)
```

Useful for logging/debugging.

---

# 10. Synchronous vs Asynchronous Invocations

### **Synchronous**

Caller waits for response.
Examples:

* API Gateway
* Application Load Balancer
* CLI invoke

### **Asynchronous**

Caller does **not** wait for response.
Examples:

* S3
* SNS
* EventBridge
* SES

Asynchronous invocations support **retries**, **DLQ**, and **destinations**.

---

# 11. Dead Letter Queue (DLQ)

DLQ stores failed asynchronous Lambda events.

Supported DLQs:

* SQS
* SNS

Used to debug failed events.

---

# 12. Trigger Lambda on S3 Object Creation/Update

Steps:

1. Go to S3 bucket
2. Enable event notification
3. Choose event (PUT, POST, COPY, DELETE)
4. Select Lambda function

Event example:

```json
{
  "Records": [
    {
      "s3": {
        "object": {"key": "file.txt"}
      }
    }
  ]
}
```

---

# 13. Trigger Lambda From AWS Application Load Balancer (ALB)

Requirements:

* Lambda must use **ALB target group** type: Lambda
* ALB listener forwards HTTP requests to Lambda

Event example:

```json
{
  "httpMethod": "GET",
  "path": "/hello",
  "headers": {}
}
```

---

# 14. Using External Libraries in Lambda

For Python:

```bash
pip install requests -t .
zip -r function.zip .
```

Upload zip to Lambda.

For Node.js:

```bash
npm install axios
zip -r function.zip .
```

---

# 15. Lambda Layers

Layers help store reusable libraries.

Use cases:

* Python dependencies
* Shared config files
* Common utilities

Example structure:

```
python/
  └── requests
```

---

# 16. Share Your Own Library

Package your custom helper functions into a **layer**, then attach it to multiple Lambda functions.

This ensures:

* Reusability
* Smaller Lambda size
* Easier maintenance

---

# 17. What is Lambda Version?

Versions = **immutable snapshots** of Lambda code.

Useful for:

* Production releases
* Rollback
* Blue-green deployment

---

# 18. What is Lambda Alias?

Alias = pointer to a version.

Example:

* Alias "prod" → Version 3
* Alias "dev" → Version 7

Aliases support **traffic shifting** (canary deployments).

---

# 19. Resource Policy vs IAM Role

### **IAM Role**

Defines what Lambda **can access**.
Example: S3, DynamoDB, RDS.

### **Resource Policy**

Defines **who can invoke Lambda**.
Example: Allow API Gateway to call Lambda.

---

# 20. Lambda in VPC

Put Lambda into a VPC when:

* Accessing RDS
* Accessing Elasticache
* Accessing internal services

Requires:

* Subnets
* Security groups
* NAT Gateway (for internet access)

---

# 21. Connecting Lambda to RDS

To connect:

1. Put Lambda inside same VPC
2. Allow SG inbound rules
3. Install DB library (pymysql, pg8000)
4. Use connection pooling OR RDS Proxy

Example Python code:

```python
import pymysql
connection = pymysql.connect(
    host='mydb.xxxxx.rds.amazonaws.com',
    user='admin',
    password='pass',
    db='testdb'
)
```

---

# 22. Reserved Concurrency vs Provisioned Concurrency

### Reserved Concurrency

* Guarantees maximum concurrency limit
* Prevents Lambda from scaling too much

### Provisioned Concurrency

* Pre-warms execution environments
* Removes cold starts completely

---

# 23. AWS Lambda Destinations

Destinations capture the **result** of async Lambda execution.

### **On Success**:

* SQS
* SNS
* EventBridge
* Another Lambda

### **On Failure**:

* SQS
* SNS
* EventBridge
* Another Lambda

Better than DLQ because DLQ stores only failures.

---


This README provides an in-depth guide on AWS Lambda, events, triggers, networking, concurrency, deployment patterns, and interview preparation.
