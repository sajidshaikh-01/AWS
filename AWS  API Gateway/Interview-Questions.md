# 🎤  API Gateway Interview Questions & Answers

### **1. Difference between REST API and HTTP API?**

REST API is feature rich but more expensive.
HTTP API is faster, cheaper, supports JWT.

### **2. What is a Mapping Template?**

A Velocity Template Language (VTL) document used to transform request/response.

### **3. What is an Integration Request?**

How API Gateway maps incoming requests to the backend.

### **4. What is a Custom Authorizer?**

A Lambda-based authentication mechanism that returns an IAM policy.

### **5. How do you secure API Gateway?**

* IAM
* API Keys
* Cognito Authorizers
* Custom Authorizers

### **6. What is Canary Deployment?**

Percentage-based rollout of new API versions.

### **7. How do you send path/query params to backend?**

Using VTL templates:

```json
$input.params('id')
```

### **8. How to achieve zero downtime in API updates?**

Use Lambda Aliases + Stage Variables.

---
