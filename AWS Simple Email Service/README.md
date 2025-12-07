# 📧 Amazon Simple Email Service (SES) – Complete Deep Dive README

Amazon Simple Email Service (SES) is a **highly scalable, cost‑effective, secure email sending and receiving service** used for:

* Transactional emails (OTP, password reset, notifications)
* Marketing and bulk campaigns
* Application-level email automation
* Email receiving and routing

This README provides a full deep dive covering configuration, identity setup, SMTP usage, automation, monitoring, and interview questions.

---

# 🧩 1. What is Amazon SES?

Amazon SES is a cloud-based email service designed for:

* Reliable delivery
* High throughput (millions of emails per day)
* Low cost
* Flexible integration via API or SMTP

It allows you to **send**, **receive**, and **track** emails.

### SES can be used through:

* AWS SDKs (API)
* SMTP endpoint (like Gmail SMTP)
* AWS CLI
* Integration with Lambda, SNS, S3, EventBridge

---

# 🌍 2. SES Regions & Availability

SES is available in selected AWS regions only. Each region has:

* Separate SMTP credentials
* Separate email identities
* Independent reputation score

---

# 🔐 3. SES Sandbox vs Production Mode

Every new SES account starts in **Sandbox Mode**.

### Sandbox limitations:

* Only verified email senders allowed
* Limited sending quota
* Limited sending rate

### To move to production:

1. Open AWS Support → **Request to increase sending limits**
2. Provide use case, website, email type
3. AWS approves → Full sending access

---

# 🆔 4. Verifying Email Identities

SES requires identity verification for:

* Email address
* Domains

---

## ✔️ 4.1 Verify Email

SES sends a verification email → click confirmation link.

---

## ✔️ 4.2 Verify Domain (Recommended for production)

SES provides DNS records:

* TXT (Domain verification)
* MX (Receiving)
* DKIM records (improve delivery)

Add DNS records in Route 53 / GoDaddy / Cloudflare.

---

# 🔏 5. Email Authentication: SPF, DKIM & DMARC

To avoid SPAM and increase deliverability:

## ✔ SPF

Authorizes SES to send emails on behalf of your domain.

```
v=spf1 include:amazonses.com ~all
```

## ✔ DKIM

Digitally signs your emails → prevents spoofing.

```
CNAME records provided by SES
```

## ✔ DMARC

Protects your domain against phishing.

```
v=DMARC1; p=none; rua=mailto:admin@domain.com
```

---

# 📤 6. Sending Emails via SES (3 Methods)

## 1️⃣ **Send using SES API (AWS SDK)**

Example (Python):

```python
import boto3
ses = boto3.client('ses')

ses.send_email(
    Source='no-reply@domain.com',
    Destination={'ToAddresses': ['user@example.com']},
    Message={
        'Subject': {'Data': 'Hello from SES'},
        'Body': {'Text': {'Data': 'Welcome to our app!'}}
    }
)
```

---

## 2️⃣ **Send using SMTP**

SMTP works with any email client.

* Use SMTP endpoint from SES console
* Create SMTP credentials

Example (Linux):

```
openssl s_client -crlf -quiet -connect email-smtp.us-east-1.amazonaws.com:465
```

---

## 3️⃣ **Send Using AWS CLI**

```
aws ses send-email \
  --from no-reply@domain.com \
  --destination ToAddresses=user@email.com \
  --message '{"Subject":{"Data":"Hello"},"Body":{"Text":{"Data":"Test"}}}'
```

---

# 📥 7. Receiving Emails with SES

SES can receive emails and forward them to:

* S3 bucket
* Lambda function
* SNS topic
* EventBridge rule

## Example Workflow:

1. SES receives email at [info@domain.com](mailto:info@domain.com)
2. Stores raw email in S3
3. Lambda extracts attachments
4. SNS sends mobile notification

---

# 📊 8. SES Analytics and Monitoring

SES integrates with:

* **CloudWatch Metrics** (Delivery, Bounce, Complaint, Reject)
* **CloudWatch Alarms** (High bounce or complaint rate)
* **Event Publishing to SNS** (Track each email event)

### Common Metrics:

* Delivery attempts
* Bounce rate
* Complaint rate
* Rejected messages

---

# 🔄 9. Email Templates in SES

SES supports reusable templates.

```
Hi {{name}}, your OTP is {{otp}}.
```

Templates are stored in SES and can be used via SDK or CLI.

---

# 📦 10. Bulk Email Sending

SES supports bulk email delivery using:

* **Bulk templates**
* **Configuration sets**
* **Sending pools**
* **Dedicated IPs (optional)**

Used by:

* Marketing campaigns
* Newsletter systems
* Ecommerce platforms

---

# 🧰 11. Common SES Integrations

| Service     | Usage                                 |
| ----------- | ------------------------------------- |
| Lambda      | Process incoming emails               |
| S3          | Store raw emails                      |
| SNS         | Send notifications on delivery/bounce |
| EventBridge | Email event routing                   |
| CloudWatch  | Monitoring                            |
| Route 53    | DNS management (SPF, DKIM, DMARC)     |

---

