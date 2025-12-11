# 🧪 9. Real-Time Scenarios

## **Scenario 1: Secret Leaked in GitHub**

### Fix:

* Rotate credentials immediately
* Invalidate old tokens
* Use Secrets Manager & IAM roles instead of storing secrets

---

## **Scenario 2: Lambda Needs DB Credentials Without Restart**

Solution:

* Use Secrets Manager
* Retrieve secret on each invocation or cache refresh

---

## **Scenario 3: You Need Zero-Downtime Secret Rotation**

Use:

* Secrets Manager automatic rotation
* Applications reading secret dynamically (not via env variable)

---

## **Scenario 4: Multi-Region Secret Access**

Use Secrets Manager cross‑region replication.

---

## **Scenario 5: ECS Tasks Need Secrets on Startup**

Use ECS Task Definition secrets mapping.

---

# 🎤 10. Interview Questions & Answers

### **1. What is the difference between Secrets Manager and Parameter Store?**

| Secrets Manager         | Parameter Store         |
| ----------------------- | ----------------------- |
| Paid                    | Free (Standard)         |
| Automatic rotation      | No built-in rotation    |
| Feature-rich            | Basic secret management |
| Best for DB credentials | Best for config values  |

---

### **2. How does AWS Secrets Manager encrypt secrets?**

Using AWS KMS keys.

---

### **3. What is secret rotation? Why is it needed?**

Rotating secrets reduces the risk of long-term credential exposure.

---

### **4. How does Lambda securely access secrets?**

Through IAM permissions + Secrets Manager / SSM calls.

---

### **5. Why shouldn’t we store secrets in environment variables directly?**

They may leak in logs, crash dumps, or snapshots.

---

### **6. How do ECS tasks use secrets?**

Using Secret Manager references inside the task definition.

---

### **7. What happens if KMS key is disabled?**

Your application will fail to decrypt secrets.

---

### **8. How to audit secret access?**

CloudTrail logs every Secrets Manager or SSM call.

---

### **9. Can you access secrets cross‑account?**

Yes, using resource policies.

---

### **10. How do you handle secrets for CI/CD pipelines?**

Use:

* GitHub Actions → OIDC + SSM
* CodePipeline → Secrets Manager integration

---


