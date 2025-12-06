#  CloudTrail Interview Questions & Answers

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

