# AWS Cognito – Complete Deep Dive README

---

# 📘 1. What is AWS Cognito?

AWS Cognito is a fully managed service that provides:

* **User authentication** (signup, login, logout)
* **User directories**
* **Password policies & MFA**
* **Hosted UI for login**
* **JWT token generation**
* **Identity federation** (Google, Facebook, Apple, SAML)
* **Temporary AWS credentials** via Identity Pools

Cognito is used to securely authenticate users in mobile, web, and serverless applications.

---

# 🏛 2. Cognito Components

## **1. User Pool (Authentication)**

* Handles signup/login
* Stores users
* Issues **JWT tokens**: ID, Access, Refresh
* Supports MFA, password policy, attributes
* Integrates with API Gateway authorizers

## **2. Identity Pool (Authorization)**

* Provides **temporary AWS credentials** via STS
* Maps users to IAM roles
* Supports both authenticated & guest access

---

# 🔐 3. User Pool Tokens Explained

When a user logs in, Cognito returns **3 tokens**:

### **1. ID Token**

* Contains user identity info
* Used for authentication
* Sent to backend APIs

### **2. Access Token**

* Authorizes access to protected APIs
* Used by API Gateway & Lambda

### **3. Refresh Token**

* Used to obtain new ID/Access tokens
* Valid up to 30 days

---

# 🧩 4. Cognito Authentication Flow

1. User enters username/password
2. Cognito verifies credentials
3. Cognito returns ID + Access + Refresh tokens
4. Tokens are used to authenticate requests to API Gateway / backend services

---

# 🌐 5. Cognito Hosted UI

Cognito provides a **ready-made login page** with:

* Username/password
* Social logins (Google, Facebook, Apple)
* SAML Federation

You can customize branding, logo, redirects.

---

# 🔒 6. Multi-Factor Authentication (MFA)

Cognito supports:

* SMS MFA
* TOTP MFA (Google Authenticator)

You can configure:

* Optional MFA
* Required MFA

---

# 🧪 7. Cognito Triggers (Lambda Functions)

Cognito can call Lambda at specific events:

* Pre Sign-up
* Post Confirm
* Pre Authentication
* Post Authentication
* Custom Message
* Pre Token Generation
* User Migration

Example Use Cases:

* Custom validation during signup
* Enrich user attributes
* Send customized emails

---

# 🔗 8. Integrating Cognito with API Gateway

API Gateway supports Cognito as an **authorizer**.

When a user calls API Gateway:

1. They send **JWT token** in Authorization header

```
Authorization: Bearer <id_token>
```

2. API Gateway verifies signature & token
3. If valid → forwards to backend (Lambda / EC2)
4. If invalid → returns 401

---

# 🔑 9. Cognito Identity Pool (Authorization Layer)

Identity Pools allow you to:

* Grant AWS credentials to users
* Map users to IAM roles
* Give authenticated users different access than guests

Example IAM role mapping:

* Authenticated: Full DynamoDB Access
* Guest: Read-Only S3 Access

---

# 📁 10. Cognito + Lambda Example (Serverless Auth)

### Lambda receives user claims:

```python
def lambda_handler(event, context):
    claims = event['requestContext']['authorizer']['jwt']['claims']
    username = claims.get('cognito:username')
    email = claims.get('email')
    return {"user": username, "email": email}
```

---

# 🧭 11. Cognito + API Gateway Example Architecture

```
User → Cognito Hosted UI → Receives Tokens → Calls API Gateway → Lambda
```

---

# 📦 12. Real-Time Scenarios

## **Scenario 1: You need social login (Google + Facebook)**

Use Cognito Hosted UI + Federated Identity Providers.

---

## **Scenario 2: API returns 401 — token rejected**

Possible causes:

* Token expired
* User disabled
* Wrong User Pool config in API Gateway
* Token signed with old RSA keys

---

## **Scenario 3: You need user-specific permissions in AWS**

Use Identity Pools and assign IAM roles based on groups.

---

## **Scenario 4: You want custom signup validation**

Use Pre-Signup trigger.

---

## **Scenario 5: You want to migrate users from old system**

Use User Migration trigger.

---



