# AWS S3 – Complete Deep Dive README (Buckets, Object Properties, Versioning, Static Hosting, Transfer Acceleration, Replication)
---
# ☁️ **What is Amazon S3?**

Amazon S3 (Simple Storage Service) is an **object storage service** designed for:

* Infinite scalability
* 99.999999999% (11 9's) durability
* Global availability

S3 stores data as **objects inside buckets**, not as files in directories.

Each object = Data + Metadata + Key + Version ID

---

# 🪣 **S3 Bucket Overview**

An S3 bucket is a global namespace container.

* Bucket names must be globally unique
* Bucket belongs to exactly **one region**
* Objects inside the bucket can have unlimited size (up to 5TB each)

---

# 📌 **S3 Object Properties (Deep Explanation)**

Each object in S3 contains multiple properties:

## 1️⃣ **Object Key**

This is the full path of the object.

```
example-folder/images/file1.png
```

Keys simulate folder structure (S3 has no real folders).

## 2️⃣ **Version ID**

Unique identifier for each version of an object.
Used for recovery and auditing.

## 3️⃣ **ETag (Entity Tag)**

* A fingerprint/hash of the object
* Used for detecting changes
* For small files = MD5 checksum

## 4️⃣ **Metadata**

Two types:

* System metadata (Content-Type, Last-Modified)
* User metadata (custom key-value pairs)

## 5️⃣ **Storage Class**

Defines the cost + availability of object.
Examples:

* Standard
* Standard-IA
* One Zone IA
* Glacier / Deep Archive

## 6️⃣ **ACL / Bucket Policy**

Permissions on object level.
ACL = Legacy access model.
Policies = JSON-based security rules.

## 7️⃣ **Encryption Status**

S3 supports:

* SSE-S3 (AES-256)
* SSE-KMS
* SSE-C

---

# 🔁 **S3 Versioning – Deep Explanation**

Versioning protects your data from accidental:

* Deletes
* Overwrites
* Corruption

### **What happens when versioning is enabled?**

Every modification creates a **new version**.

### When you DELETE an object:

* A *delete marker* is added
* Object is not removed
* You can restore older version anytime

### Benefits:

* Protect against accidental deletes
* Restore old files
* Required for CRR/SRR

### Commands:

Enable versioning:

```
aws s3api put-bucket-versioning --bucket mybucket --versioning-configuration Status=Enabled
```

---

# 🌐 **Static Website Hosting in S3**

S3 can host static websites using:

* HTML
* CSS
* JS
* Images

### Steps:

1. Create a bucket
2. Bucket name must match domain (for custom domains)
3. Upload website files
4. Enable **Static website hosting**
5. Make objects public (Bucket Policy)
6. Access via website endpoint:

```
http://mybucket.s3-website-us-east-1.amazonaws.com
```

### Limitations:

❌ Cannot run server-side code
❌ No HTTPS by default (requires CloudFront)

---

# ⚡ **S3 Transfer Acceleration**

A feature that uses CloudFront’s globally distributed **edge locations** to speed up uploads.

### How it works:

1. User uploads file to nearest AWS edge location
2. AWS uses **AWS backbone network** to deliver data to S3 bucket

### Benefits:

* High-speed uploads from distant locations
* Uses TCP optimizations

### Usage endpoint:

```
bucketname.s3-accelerate.amazonaws.com
```

---

# 🔁 **S3 Replication (Deep Explanation)**

Replication copies objects **automatically** from one bucket to another.

Two major types:

* **Same-Region Replication (SRR)**
* **Cross-Region Replication (CRR)**

Replication requires:

* Versioning enabled on source & destination
* IAM Role for S3 to replicate objects
* Supported storage classes

---

# 🔁 1️⃣ **Same-Region Replication (SRR)**

SRR replicates objects **within the same AWS region**.

### Use Cases:

* Log aggregation
* Multi-account backup
* Enforcing compliance
* Performance optimization

### Data Flow:

```
S3 Bucket (Source, us-east-1) → S3 Bucket (Destination, us-east-1)
```

---

# 🌍 2️⃣ **Cross-Region Replication (CRR)**

CRR copies objects to **another AWS region** automatically.

### Use Cases:

* Disaster recovery
* Global distribution
* Compliance
* Reduced latency for global users

### Data Flow:

```
S3 Bucket (Source, us-east-1) → S3 Bucket (Destination, ap-south-1)
```

### Important Notes:

* Replication is **asynchronous**
* Existing objects are not replicated unless you enable "replicate existing objects"

---

# 🧠 SRR vs CRR – Summary Table

| Feature   | SRR                 | CRR                     |
| --------- | ------------------- | ----------------------- |
| Region    | Same region         | Different regions       |
| Latency   | Lower               | Higher (network travel) |
| DR        | ❌ Not ideal         | ✔ Excellent             |
| Cost      | Lower               | Higher                  |
| Use Cases | Logging, compliance | Global backups, DR      |

---



