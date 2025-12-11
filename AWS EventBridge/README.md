# Amazon EventBridge – Complete Deep Dive README

This README explains Amazon EventBridge in detail, including rules, buses, event patterns, targets, scheduling, integrations, pipes, schema registry, retries, failures, real-time scenarios, and interview questions.

---

# 📘 1. What is Amazon EventBridge?

Amazon EventBridge is a **serverless event bus** used for building event-driven applications. It routes events from AWS services, SaaS applications, and custom applications to targets like:

* Lambda
* Step Functions
* SQS
* SNS
* Kinesis
* API Gateway
* EventBridge Pipes
* ECS Tasks

EventBridge helps decouple microservices using an asynchronous architecture.

---

# 🚌 2. Event Buses in EventBridge

EventBridge has **3 types** of event buses:

### **1. Default Event Bus**

Receives events from AWS services automatically.

### **2. Custom Event Bus**

Created by user applications to send custom events.

```bash
aws events create-event-bus --name MyCustomBus
```

### **3. Partner Event Bus**

Used to receive events from third‑party SaaS apps like Zendesk, Okta, Shopify.

---

# 🎯 3. EventBridge Rules

Rules match events and route them to targets.

A rule contains:

* Event Pattern (conditions)
* Target (Lambda, SQS, etc.)

### Example Rule Pattern (Lambda trigger when EC2 stops):

```json
{
  "source": ["aws.ec2"],
  "detail-type": ["EC2 Instance State-change Notification"],
  "detail": {"state": ["stopped"]}
}
```

---

# 🔄 4. Event Patterns in EventBridge

Event patterns filter events based on:

* source
* detail-type
* detail fields
* AWS service events

### Example: Trigger on S3 file upload

```json
{
  "source": ["aws.s3"],
  "detail": {"object": {"size": [{"numeric": [">", 0]}]}}
}
```

---

# 🎯 5. Event Targets

A rule can send events to:

* Lambda
* SNS
* SQS
* Step Functions
* Kinesis
* API Gateway
* ECS
* EventBridge Bus (cross-account)

EventBridge can route **one event to multiple targets**.

---

# ⏰ 6. EventBridge Scheduled Rules (Cron/Schedule)

EventBridge can run cron jobs **without Lambda timers**.

### Example: Run every 5 minutes

```cron
rate(5 minutes)
```

### Example: Daily at 12:00 AM

```cron
cron(0 0 * * ? *)
```

---

# 🔗 7. EventBridge Pipes

Pipes provide **point‑to‑point integration** between event sources and targets with:

* Filtering
* Enrichment (Lambda, API calls)
* Transformation

### Example source → target using pipe:

SQS → Lambda
DynamoDB Stream → Kinesis
Kafka → Step Functions

---

# 🧪 8. Sending Custom Events to EventBridge

### CLI Example

```bash
aws events put-events --entries '[{
  "Source": "myapp.order",
  "DetailType": "OrderCreated",
  "Detail": "{\"orderId\":123}",
  "EventBusName": "MyCustomBus"
}]'
```

### Lambda Example

```python
import boto3, json
client = boto3.client('events')
client.put_events(
  Entries=[{
    'Source':'myapp.order',
    'DetailType':'OrderCreated',
    'Detail': json.dumps({'orderId': 123}),
    'EventBusName':'MyCustomBus'
  }]
)
```

---

# 📘 9. Schema Registry

EventBridge Schema Registry stores **schemas for events**.

Benefits:

* Auto‑generated code bindings
* Discover event structures
* Enforces schema in applications

---

# 🔁 10. EventBridge Retry Logic

EventBridge automatically retries failed targets:

* 24 hours retry window
* Exponential backoff

If failures continue → send to **DLQ** (SQS).

---

# 🗂 11. Dead Letter Queue (DLQ)

EventBridge rules support DLQs for failed event deliveries.

DLQ Target:

* SQS
* SNS

---

# 🌍 12. Cross-Account & Cross-Region EventBridge

EventBridge supports secure event sharing across:

* **AWS accounts**
* **AWS regions**

Use resource policies to allow sending events between accounts.

---

# 📂 13. Real-Time Use Cases of EventBridge

* Decoupled microservices
* Trigger Lambda from S3, EC2 events
* Automation workflows (Start/Stop EC2, RDS)
* SaaS ↔ AWS integration
* Real‑time monitoring workflows
* Data pipelines (Kafka / DynamoDB Streams → EventBridge Pipes → Targets)

---

