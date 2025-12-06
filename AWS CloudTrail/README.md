# AWS CloudTrail – Complete README

---

# 🌐 What is AWS CloudTrail?

AWS CloudTrail is a service that records all **API calls and events** that occur in your AWS account.
It helps with:

* Security auditing
* Compliance
* Operational troubleshooting

CloudTrail logs **who did what, when, and from where** across AWS.

---

# 🧱 Key Features of CloudTrail

## 🔹 1. Event History

Stores the last 90 days of management events.
Useful for quick auditing.

---

## 🔹 2. CloudTrail Trails

A *Trail* is a configuration that delivers log files to an S3 bucket.
You can:

* Record events across **all regions** (recommended)
* Send logs to **CloudWatch Logs** for real-time alerts

---

## 🔹 3. Types of Events

CloudTrail captures 3 main types of events:

### **1️⃣ Management Events**

Administrative actions like:

* Creating EC2 instances
* Modifying IAM policies
* Creating S3 buckets

### **2️⃣ Data Events**

High-volume operations:

* S3 object-level access (GetObject, PutObject)
* Lambda function execution events

### **3️⃣ Insights Events**

Detect unusual activity such as:

* Sudden spike in API calls
* Errors in IAM access patterns

---

# 🗂️ CloudTrail Log Structure

Each event contains:

* **eventTime** – When the action happened
* **eventSource** – Service (e.g., s3.amazonaws.com)
* **eventName** – API action (e.g., PutObject)
* **userIdentity** – Who performed the action
* **sourceIPAddress** – From where
* **requestParameters** – What was requested

---

# 🏗️ CloudTrail Architecture Workflow

1. User or service performs an action.
2. CloudTrail records the API call.
3. Log delivered to S3 bucket.
4. (Optional) Sent to CloudWatch Logs.
5. Alerts triggered via CloudWatch or SNS.

---

# 🔐 Security Benefits of CloudTrail

* Detect unauthorized access
* Track changes to IAM, EC2, S3, VPC
* Monitor failed login attempts
* Investigate incidents
* Mandatory for compliance (HIPAA, PCI, SOC)

---

# 🧪 Real-World Use Cases

### ⭐ Detect who deleted an EC2 instance.

### ⭐ Track S3 object access.

### ⭐ Find source IP of failed console logins.

### ⭐ Integrate with SIEM tools for security analysis.

### ⭐ Trigger CloudWatch alarm on suspicious activity.

---

# 🛠️ CloudTrail CLI Commands

### List trails:

```
aws cloudtrail list-trails
```

### Create a trail:

```
aws cloudtrail create-trail --name mytrail --s3-bucket-name mybucket
```

### Start logging:

```
aws cloudtrail start-logging --name mytrail
```

### Lookup events:

```
aws cloudtrail lookup-events --lookup-attributes AttributeKey=EventName,AttributeValue=ConsoleLogin
```

---

