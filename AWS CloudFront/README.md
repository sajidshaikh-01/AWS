# AWS CloudFront – Complete Deep Dive README (Distributions, Invalidation, Security, Routing, Geo-Restrictions, Error Handling)
---
# 🌐 1. What is Amazon CloudFront?

Amazon CloudFront is a **global content delivery network (CDN)** that securely delivers:

* Static content (HTML, CSS, JS, images)
* Dynamic content
* API responses
* Videos & streaming

CloudFront uses a network of **edge locations** worldwide to cache and deliver content with low latency.

---

# 🏗️ 2. CloudFront Distribution Creation (Step-by-Step)

A CloudFront distribution defines:

* **Origin** (S3, EC2, ALB, API Gateway)
* Cache behavior
* Security settings

## 🚀 Steps to Create a Distribution:

1. Go to **CloudFront Console** → Create Distribution
2. Choose Origin Type:

   * S3 Bucket
   * Application Load Balancer
   * EC2 Instance
   * Custom Origin
3. Set **Origin Domain**
4. Configure Cache Behavior:

   * Allowed HTTP methods
   * TTL (min, default, max)
   * Cache key
5. Enable **HTTPS** using SSL certificates (ACM)
6. Optional:

   * Enable WAF
   * Enable Logging
   * Add Geo Restrictions

Once created, CloudFront provides a **Distribution Domain**:

```
d123example.cloudfront.net
```

Use this domain to serve content globally.

---

# 🧹 3. CloudFront Invalidation (Deep Explanation)

Invalidation removes specific files from CloudFront cache so users get the latest version.

## When to Invalidate?

* Updating CSS/JS/HTML files
* Fixing a bug in deployed static content
* Purging outdated assets

## Create an Invalidation:

1. CloudFront Console → Distribution
2. Choose **Invalidations → Create Invalidation**
3. Add object paths

### Examples:

Invalidate single file:

```
/index.html
```

Invalidate entire site:

```
/*
```

### CLI Example:

```
aws cloudfront create-invalidation --distribution-id ABC123 --paths "/index.html"
```

---

# 🔐 4. Make EC2/ALB Accessible **Only** from CloudFront

You can restrict ALB/EC2 origin access to CloudFront using:

## Method 1: CloudFront Managed Prefix List

Add to Security Group:

```
Source: com.amazonaws.global.cloudfront.origin-facing
```

This ensures **only CloudFront** can call your origin.

## Method 2: Custom Header Validation

1. Add a custom header in CloudFront:

```
x-origin-verify: secret123
```

2. Validate against ALB/EC2 using:

* NGINX configuration
* Application code logic

---

# 🔒 5. S3 Private Bucket with CloudFront (OAC Recommended)

To prevent direct S3 access, use **Origin Access Control (OAC)**.

## Steps:

1. Create CloudFront distribution with S3 origin
2. Enable **Origin Access Control (OAC)**
3. Update S3 bucket policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCloudFrontAccess",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudfront.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::mybucket/*",
      "Condition": {
        "StringEquals": {
          "AWS:SourceArn": "arn:aws:cloudfront::123456789:distribution/ABC123"
        }
      }
    }
  ]
}
```

4. Disable public access on S3 bucket.

Result → **Private S3 bucket accessible only via CloudFront.**

---

# 📁 6. CloudFront Path-Based Routing

CloudFront allows routing requests to different origins based on URL path patterns.

## Example Use Case:

* `/api/*` → API Gateway/ALB
* `/images/*` → S3
* `/static/*` → S3

## Example Behaviors:

```
Behavior 1: Path Pattern /images/* → S3 Bucket
Behavior 2: Path Pattern /api/* → ALB
Behavior 3: Default Behavior /* → S3
```

## Importance:

* Multi-origin architectures
* Microservices
* Hybrid deployments

---

# ❌ 7. CloudFront Custom Error Pages

You can show custom error pages instead of default CloudFront error responses.

## Common Errors that can be Custom Handled:

* 403 Forbidden
* 404 Not Found
* 500 Server Error

## Steps:

1. Go to **Error Pages → Create Custom Error Response**
2. Choose error code (e.g., 404)
3. Set a custom page: `/errors/404.html`
4. Optional: Customize TTL

This greatly improves user experience.

---

# 🌍 8. Geo Restriction – Control Access by Country

CloudFront Geo Restriction (Geo Blocking) allows you to allow or block specific countries.

## Two Modes:

### Allowlist → Allow only certain countries

### Blocklist → Block certain countries

## Steps:

1. CloudFront → Distribution → Restrictions
2. Edit Geo Restrictions

## Example:

* Allow only: US, UK, IN
* Block: CN, RU, KP

Used for:

* Licensing
* Compliance
* Regional content control

---

# 📴 9. How to Disable a CloudFront Distribution

You cannot delete a distribution until it is disabled.

## Steps to Disable:

1. CloudFront Console → Distribution
2. Choose **Disable**
3. Wait for status → **Disabled** (takes a few minutes)
4. Now you can delete it

---




