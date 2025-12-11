
# 🧪 1. Real-Time CloudWatch Scenario Questions

## **Scenario 1: CPU Spikes But You Get No Alert — Why?**

### Possible Issues:

* Alarm configured on wrong dimension
* Wrong evaluation period
* Metric missing (EC2 stopped)
* Alarm in “INSUFFICIENT DATA” state

---

## **Scenario 2: Lambda Logs Are Not Appearing in CloudWatch**

### Troubleshooting:

* IAM role missing `logs:CreateLogGroup` / `logs:CreateLogStream` / `logs:PutLogEvents`
* VPC misconfiguration (NAT required for logs in VPC‑enabled Lambda)

---

## **Scenario 3: CloudWatch Agent Is Not Sending Logs**

### Fix:

* Wrong file path
* Permission issues
* Agent needs restart
* IAM role missing required permissions

---

## **Scenario 4: Billing Exceeded But No Email Alert**

### Fix:

* Billing alerts not enabled
* SNS subscription not confirmed
* Wrong region (billing metrics only in us‑east‑1)

---
