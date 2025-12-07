# 🧠 SES Interview Questions (With Answers)

### 1. What is SES used for?

Sending and receiving transactional and marketing emails.

### 2. How do you verify a domain in SES?

Add TXT and DKIM CNAME records to DNS.

### 3. What is the SES Sandbox environment?

A restricted mode allowing sending only to verified identities.

### 4. How do you move out of Sandbox?

Request from AWS Support with justification.

### 5. What is the difference between API and SMTP sending?

API = faster, more secure
SMTP = compatible with traditional email clients.

### 6. How does SES prevent spam?

Using SPF, DKIM, DMARC.

### 7. What is a bounce rate?

Percentage of undeliverable emails.
High bounce → SES may throttle or block your account.

### 8. How do you send bulk emails efficiently?

Use SES email templates and configuration sets.

### 9. Can SES receive emails?

Yes — using SES inbound email service.

### 10. What is reputation management in SES?

Monitoring sender metrics to maintain email deliverability.

### 11. What causes SES to throttle sending?

High bounce or complaint rates.

### 12. What is DKIM?

Digital signature for email authenticity.

### 13. Can SES encrypt outgoing emails?

Not directly. Application layer must handle encryption.

### 14. How to track SES email delivery events?

Publish events to SNS, EventBridge, or CloudWatch.

### 15. Does SES support attachments?

Yes — by using MIME encoded emails.

---

