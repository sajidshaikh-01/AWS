# 🎤. Interview Questions & Answers

### **1. What is the difference between User Pools and Identity Pools?**

| User Pool                   | Identity Pool                     |
| --------------------------- | --------------------------------- |
| Handles authentication      | Handles AWS authorization         |
| Returns JWT tokens          | Returns temporary AWS credentials |
| Integrates with API Gateway | Integrates with STS               |

---

### **2. What tokens does Cognito generate?**

* ID Token
* Access Token
* Refresh Token

---

### **3. How does API Gateway validate Cognito tokens?**

Uses JWT signature + issuer + audience checks.

---

### **4. What is a Cognito Trigger?**

Lambda functions that run during user authentication/registration events.

---

### **5. How do you secure APIs with Cognito?**

Use User Pool Authorizer in API Gateway.

---

### **6. How do you handle token expiration?**

Use Refresh Token to get new ID/Access tokens.

---

### **7. Can Cognito integrate with Active Directory?**

Yes — using SAML federation.

---

### **8. How do you migrate users from an old app?**

Use Cognito User Migration Trigger.

---

### **9. How do you reset a user password?**

Use Forgot Password flow or admin reset APIs.

---

### **10. When should you choose Cognito over OAuth providers?**

When you need:

* Managed user directory
* Federated logins
* Secure API Gateway integration
* Automatic token generation
