---

# 🧠 Advanced IAM Interview Questions (With Answers)

## **Q1: What is the difference between identity-based and resource-based policies?**

* **Identity-based policy** → Attached to users, groups, or roles.
* **Resource-based policy** → Attached directly to AWS resources (e.g., S3 bucket policy).

## **Q2: What is STS AssumeRole?**

AWS STS (Security Token Service) allows temporary credentials.

```
aws sts assume-role --role-arn arn:aws:iam::12345:role/dev-role --role-session-name test
```

Used for:

* Cross-account access
* Temporary elevated privileges
* Applications needing temporary credentials

## **Q3: What is Permission Boundaries?**

A permission boundary **limits the maximum permissions** a user or role can have.
Used to prevent privilege escalation.

## **Q4: What is Access Advisor in IAM?**

Shows which AWS services a user/role has accessed and when.
Helps identify unused permissions.

## **Q5: Difference between Inline and Managed policies?**

| Inline Policy               | Managed Policy                    |
| --------------------------- | --------------------------------- |
| Attached to ONE identity    | Reusable across identities        |
| Hard to maintain            | Easy to maintain                  |
| Deleted if identity deleted | Stays even if identity is deleted |

## **Q6: What is IAM Conditions?**

Conditions add extra constraints in policies.
Example:

* Restrict access by IP
* Allow only MFA users
* Time-based restrictions

Example:

```json
"Condition": {
  "Bool": {"aws:MultiFactorAuthPresent": "true"}
}
```

## **Q7: How to enforce MFA on an IAM user?**

Use a policy that denies all actions unless MFA is enabled.

```json
{
  "Effect": "Deny",
  "Action": "*",
  "Resource": "*",
  "Condition": {
    "BoolIfExists": {"aws:MultiFactorAuthPresent": "false"}
  }
}
```

## **Q8: What is credential report?**

A report listing:

* Users
* Password age
* MFA status
* Access key age
* Last used date

Command:

```
aws iam generate-credential-report
aws iam get-credential-report
```

## **Q9: What happens if a user belongs to multiple groups with different permissions?**

AWS merges all permissions.
But **explicit deny always overrides allow**.

## **Q10: What is IAM Access Analyzer?**

A tool that identifies resources that are publicly accessible or shared outside the account.
Useful for security audits.

## **Q11: How do you restrict an IAM role to assume only within specific AWS accounts?**

Use a trust policy with allowed account IDs.

```json
"Principal": {"AWS": "arn:aws:iam::123456789012:root"}
```

## **Q12: What is SCP (Service Control Policy)?**

Policies used in **AWS Organizations** to set permission guardrails for multiple AWS accounts.

* Apply to all accounts or OU (Organizational Units)
* Cannot grant permissions, only restrict them

## **Q13: What is IAM Policy Simulator?**

A tool to test IAM policies without applying them.
Useful for debugging permission issues.

## **Q14: What is difference between aws:username and aws:userid?**

* **username** → human-readable
* **userid** → unique internal identifier

## **Q15: What is role chaining?**

When one role assumes another role.
Limit: Maximum duration becomes **1 hour**.

## **Q16: Difference between S3 Bucket Policy and IAM Policy?**

| IAM Policy                        | S3 Bucket Policy                   |
| --------------------------------- | ---------------------------------- |
| Attached to user/role/group       | Attached to S3 bucket              |
| Controls what identity can access | Controls who can access the bucket |
| Cannot make bucket public         | Can make bucket public             |

## **Q17: When should you use IAM Roles vs Access Keys?**

### Use **IAM Role** when:

* Running on EC2, Lambda, ECS
* Need temporary credentials
* Want auto-rotated keys

### Use **Access Keys** only when:

* External applications interact with AWS
* You cannot attach a role (rare cases)

## **Q18: What is the maximum number of IAM users allowed?**

5,000 per account (soft limit).

## **Q19: What is a trust policy?**

A policy defining **who can assume a role**.

Example:

```json
{
  "Effect": "Allow",
  "Principal": {"Service": "ec2.amazonaws.com"},
  "Action": "sts:AssumeRole"
}
```

## **Q20: Explain identity federation?**

Allows users to log into AWS using external identity providers:

* SAML
* Google
* Active Directory
* Cognito

No AWS account required for users.

---
