# AWS IAM (Identity and Access Management) – Complete README
---

# 🔐 **What is IAM?**

AWS IAM (Identity and Access Management) is a global service that securely manages access to AWS resources.

IAM allows you to:

* Create users
* Create groups
* Assign permissions using policies
* Create roles for AWS services
* Enable MFA
* Manage identity federation (SSO, AD, Google Workspace, etc.)

IAM is **global** → not region‑specific.

---

# 🧱 **IAM Core Components**

## 1️⃣ **IAM Users**

Represents a person or application.

* Has username + password (for console)
* Can have Access Keys (for CLI/API)

Use cases:

* Developer accounts
* Automation scripts using access keys

---

## 2️⃣ **IAM Groups**

A collection of users. Permissions assigned to groups apply to all members.

Example groups:

* `Developers`
* `Admins`
* `DevOps`
* `ReadOnly`

---

## 3️⃣ **IAM Policies**

JSON documents that define **Allow/Deny** permissions.

### Example Policy (Allow S3 Read):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:ListBucket", "s3:GetObject"],
      "Resource": "*"
    }
  ]
}
```

---

## 4️⃣ **IAM Roles**

Roles are like users but **cannot log in**. They assume temporary credentials.

Used by:

* EC2 instances
* Lambda functions
* ECS tasks
* Cross‑account access

### Example use case:

Attach an IAM role to EC2 to allow it to access S3 without storing access keys.

---

## 5️⃣ **IAM Identity Providers (Federation)**

Allows external logins into AWS via:

* SAML 2.0
* Google Workspace
* Active Directory
* Amazon Cognito

---

# 🔐 **Types of IAM Policies**

### 1️⃣ **AWS Managed Policies**

Created and managed by AWS.
Examples:

* `AmazonS3ReadOnlyAccess`
* `AdministratorAccess`

### 2️⃣ **Customer Managed Policies**

Custom policies created by your organization.

### 3️⃣ **Inline Policies**

Attached directly to one user or role.
Not recommended for large systems.

---

# 🔐 **IAM Access Keys**

Used for CLI, SDK, Terraform, automation.

Components:

* Access Key ID
* Secret Access Key

### Check configured IAM user:

```
aws sts get-caller-identity
```

### Create access key (console):

IAM → Users → Security Credentials → Create Access Key

**Never commit access keys to GitHub.**

---

# 🔐 **IAM Password Policy**

You can enforce:

* Minimum length
* Uppercase/lowercase
* Numbers & symbols
* Password expiration
* Prevent reuse

---

# 🔐 **IAM MFA (Multi-Factor Authentication)**

Adds an additional layer of security.

Devices:

* TOTP Apps (Google Authenticator, Authy)
* Hardware devices (YubiKey)

Enable MFA for:

* Root user
* Admin users

---

# 🏛️ **IAM Best Practices (AWS Recommended)**

### ✅ DO

* Enable MFA for all users
* Use IAM roles instead of access keys
* Follow least-privilege model
* Rotate access keys regularly
* Use groups to assign permissions
* Use AWS Organizations for multi‑account setups

### ❌ DO NOT

* Use root user for daily tasks
* Store access keys in code
* Attach `AdministratorAccess` everywhere

---

# 🔐 **IAM Permission Evaluation Logic**

Order of evaluation:
1️⃣ Explicit **Deny** (overrides everything)
2️⃣ Explicit **Allow**
3️⃣ Default **Deny**

Example:

* If a user has an Allow via Group
* But an Inline policy has Deny → Deny always wins

---

# 🌍 **Real-World IAM Use Cases**

### 🟦 **EC2 accessing S3 securely**

Attach IAM Role → avoids hardcoding access keys.

### 🟪 **CI/CD pipeline using IAM roles**

CodePipeline + CodeBuild use IAM Roles.

### 🟩 **Read-only access for auditors**

Assign AWS Managed Policy → `ReadOnlyAccess`.

### 🟥 **Cross-account access for DevOps**

Use IAM role assumption (STS AssumeRole).

---

# 🔐 **IAM Inline Examples for DevOps**

### Allow EC2 to read S3 bucket

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:*",
      "Resource": "*"
    }
  ]
}
```

### Deny deleting objects in S3

```json
{
  "Effect": "Deny",
  "Action": "s3:DeleteObject",
  "Resource": "*"
}
```

---

# 🧪 **IAM CLI Commands**

### List IAM users:

```
aws iam list-users
```

### Create a user:

```
aws iam create-user --user-name devuser
```

### Attach policy:

```
aws iam attach-user-policy \
  --user-name devuser \
  --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
```

### Create access key:

```
aws iam create-access-key --user-name devuser
```

---

# 🧠 **IAM Interview Questions (Quick Answers)**

### ⭐ What is IAM?

Service for managing access to AWS resources.

### ⭐ Difference between user & role?

| User                  | Role                  |
| --------------------- | --------------------- |
| Login possible        | Cannot login          |
| Long-term credentials | Temporary credentials |
| Used by people        | Used by AWS services  |

### ⭐ What is least privilege?

Giving only required permissions — nothing more.

### ⭐ What is an inline policy?

A policy directly attached to a single user/role (not reusable).

### ⭐ What is the root user?

The main account with **unrestricted power**. Should be used only for:

* Billing
* Account closure
* Support plans
* MFA setup

---

# 📌 **Summary**

IAM is the foundation of AWS security. It provides identities, permissions, roles, MFA, password policies, and best practices needed for secure cloud operations.

