# AWS Lambda Scenario-Based & Real-Time Interview Questions
---

## **Scenario 1: Your Lambda Function Keeps Timing Out — What Will You Check?**

### Possible Causes:

* Lambda in VPC missing NAT Gateway → cannot reach internet
* Incorrect security group rules for RDS/ElastiCache
* Long external API calls
* Timeout too low
* Large Lambda package causing cold starts

### How to Answer:

To troubleshoot Lambda timeout:

1. Check **CloudWatch logs** to see where the execution hangs.
2. If Lambda runs inside a VPC:

   * Check private subnet routing to the NAT gateway
   * Verify security group inbound rules
3. Increase timeout if necessary.
4. Reduce cold starts using **Provisioned Concurrency**.

---

## **Scenario 2: Too Many Database Connections From Lambda — What Will You Do?**

### Why it Happens:

Each Lambda execution creates a new connection → overloads RDS.

### How to Answer:

To fix connection exhaustion:

1. Use **RDS Proxy** to pool and reuse connections.
2. Reuse database connection outside handler:

```python
# Global connection reuse
db = connect()
```

3. Limit Lambda concurrency.
4. Optimize database connection lifetime.

---

## **Scenario 3: Trigger Lambda Only When a JSON File Is Uploaded to S3**

### How to Answer:

Use S3 event filtering:

```json
{"suffix": ".json"}
```

OR inside Lambda:

```python
if not key.endswith('.json'):
    return "Ignore file"
```

---

## **Scenario 4: Lambda Needs 20 Minutes to Complete — What Will You Do?**

Lambda max timeout = **15 minutes**.

### Solution:

* Use **Step Functions** for long-running workflows.
* Use **AWS Fargate** for long jobs.
* Use **AWS Batch** for heavy compute.

---

## **Scenario 5: Lambda Fails Randomly — How Will You Debug?**

### Steps:

1. Analyze CloudWatch Logs.
2. Enable AWS X-Ray for tracing.
3. Validate event payload structure.
4. Add DLQ or Destinations to capture failed events.
5. Check concurrency metrics.

---

## **Scenario 6: Deploy Lambda Update With Zero Downtime**

### Solution:

* Use Lambda **Versions**
* Add **Aliases** (prod, dev)
* Implement **Canary Deployments** (traffic shifting)

---

## **Scenario 7: 15 Lambda Functions Need the Same Library**

### Solution:

Use **Lambda Layers**:

1. Package library
2. Upload as layer
3. Attach layer to all functions

---

## **Scenario 8: Restrict Who Can Invoke Your Lambda**

### Solution:

Use **Resource Policies**:

* Allow API Gateway
* Deny public access

---

## **Scenario 9: Lambda Needs Access to DynamoDB, S3, and Parameter Store**

### Solution:

Use IAM role with **least privilege**:

* DynamoDB: specific table access
* S3: specific bucket
* SSM: specific parameter path

---

## **Scenario 10: Lambda Must Process Messages in Order**

### Solution:

Use **SQS FIFO Queue** → preserves message ordering.

---

# Additional Real-Time Questions

### **1. What causes Cold Starts in Lambda?**

A new execution environment is created → runtime loading, initialization.

### **2. How to Reduce Lambda Cold Starts?**

* Provisioned Concurrency
* Reduce package size
* Use lighter runtimes

---

### **3. Why Lambda is not ideal for large DB transactions?**

Because Lambda can scale quickly → opens too many DB connections.

---

### **4. How to Debug Lambda Errors?**

* CloudWatch Logs
* AWS X-Ray
* DLQ
* Destinations
* Lambda Insights

---

### **5. What is the difference between DLQ and Destinations?**

| DLQ                 | Destinations               |
| ------------------- | -------------------------- |
| Only for failures   | For success & failure      |
| Stores raw messages | Stores execution result    |
| Only SNS/SQS        | SNS/SQS/Lambda/EventBridge |

---

### **6. What is Provisioned Concurrency?**

Pre-warms Lambda environments → no cold starts.

---

### **7. What happens if Lambda exceeds concurrency limits?**

Lambda throws **429 throttling error**.

---

### **8. How to secure Lambda running in VPC?**

* Use private subnets
* Security groups
* NAT Gateway for internet
* VPC endpoints for AWS services

---

### **9. Maximum Lambda Response Size**

* Sync: 6 MB
* Async: 256 KB

---

### **10. Can Lambda invoke another Lambda? How?**

Yes.

```python
boto3.client('lambda').invoke(FunctionName='AnotherLambda')
```

---

