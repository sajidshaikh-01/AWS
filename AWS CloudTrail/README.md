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

# 🧠 CloudTrail Interview Questions & Answers

## **Q1: What is CloudTrail used for?**

CloudTrail records all API activity in AWS for auditing, monitoring, and security analysis.

---

## **Q2: What is the difference between CloudTrail and CloudWatch?**

| CloudTrail               | CloudWatch                       |
| ------------------------ | -------------------------------- |
| Logs API calls           | Monitors metrics & logs          |
| Who, what, when, where   | Performance and operational data |
| Primarily security/audit | Monitoring & alerting            |

---

## **Q3: What is a CloudTrail Trail?**

A configuration that delivers log files to S3 and optionally CloudWatch.

---

## **Q4: What are Management Events?**

Events related to administrative tasks like EC2 creation, IAM changes, VPC modifications.

---

## **Q5: What are Data Events?**

Events related to resource-level activity like:

* S3 object-level access
* Lambda function execution

They are **not logged by default** due to cost.

---

## **Q6: What are CloudTrail Insights?**

Detect unusual or unexpected activity patterns.
Example:

* Sudden IAM access failures
* API usage spikes

---

## **Q7: Does CloudTrail work across all AWS Regions?**

Yes. Recommended to enable **multi-region trail** to cover the entire account.

---

## **Q8: Where are CloudTrail logs stored?**

In an S3 bucket specified in the Trail.

---

## **Q9: What is Lookup Events in CloudTrail?**

Allows querying the event history for the last 90 days.
Useful for:

* Investigating incidents
* Searching API activities

---

## **Q10: Can CloudTrail trigger alerts?**

Yes. By integrating CloudTrail with **CloudWatch Logs** → create metric filters → send SNS notifications.

---

## **Q11: Is CloudTrail enabled by default?**

CloudTrail event history is enabled by default for 90 days.
But **Trails are not** — must be manually created to store logs in S3.

---

## **Q12: How does CloudTrail help in security incidents?**

Provides:

* Audit history
* Exact API actions performed
* IP addresses of attackers
* IAM details used

---

## **Q13: What is the difference between CloudTrail and Config?**

| CloudTrail               | AWS Config                   |
| ------------------------ | ---------------------------- |
| Logs API calls           | Tracks configuration changes |
| Who performed the action | What changed in the resource |
| Event-based              | State-based                  |

---

## **Q14: What happens if CloudTrail S3 bucket is deleted?**

CloudTrail stops delivering logs → loss of audit visibility.
(AWS recommends enabling object lock.)

---

## **Q15: Why should CloudTrail be enabled across all regions?**

To detect:

* Unauthorized activity in unused regions
* Crypto mining attacks
* Unexpected service creation

---

