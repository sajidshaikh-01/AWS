# AWS EC2 – Complete README (Instances, Types, Templates, Pricing Models, Security, Placement Groups + Interview Q&A)
---
# 🚀 **What is Amazon EC2?**

Amazon EC2 (Elastic Compute Cloud) provides scalable virtual servers (instances) in AWS.
You can launch, stop, resize, and terminate servers on demand.

---

# 🖥️ **1. EC2 Instances**

An EC2 Instance = Virtual Machine running on AWS.

Each instance has:

* vCPU
* Memory
* Storage (EBS or Instance Store)
* Network bandwidth
* OS (Linux / Windows)

Operations:

* Start
* Stop
* Reboot
* Terminate

Instances run inside **Availability Zones**.

---

# 🧩 **2. EC2 Instance Types**

Instance types are collections of CPU, RAM, storage, and network capacity.

## **Major EC2 Family Types:**

| Family       | Purpose                |
| ------------ | ---------------------- |
| **t**, **m** | General Purpose        |
| **c**        | Compute Optimized      |
| **r**        | Memory Optimized       |
| **p**, **g** | GPU / Machine Learning |
| **i**, **d** | Storage Optimized      |
| **h**, **x** | High Memory            |

Examples:

* `t2.micro` (free tier)
* `m5.large`
* `c5.xlarge`
* `r6g.2xlarge`

Naming convention:

```
family + generation + size
Example: t3.micro
```

---

# 🧬 **3. EC2 Launch Templates**

Launch templates store instance configuration such as:

* AMI
* Instance type
* Security groups
* Key pairs
* User data

Used by:

* Auto Scaling Groups
* Spot Fleet
* On-demand launches

Better alternative to Launch Configurations.

---

# ⚡ **4. Spot Instances**

Spot instances let you use unused EC2 capacity **at 70–90% discounted cost**.

**BUT:** AWS can reclaim the instance with a 2-minute warning.

Use cases:

* Batch processing
* CI/CD jobs
* Big data
* Machine learning training

Avoid for:

* Databases
* Production workloads requiring stability

---

# 💰 **5. Reserved Instances (RI)**

You commit to a 1-year or 3-year term.
Cost reduction: **up to 72% compared to On-Demand**.

Types:

* Standard RI (highest discount)
* Convertible RI (change instance family/type)
* Scheduled RI (deprecated)

Best for:

* Stable workloads
* Always-running apps

---

# 💵 **6. Savings Plans**

More flexible than Reserved Instances.
Commit to spend **$ per hour** for 1–3 years.

Types:

* Compute Savings Plan
* EC2 Instance Savings Plan

Applies automatically across:

* EC2
* Fargate
* Lambda

---

# 🏠 **7. Dedicated Host**

Physical EC2 server dedicated **only for your account**.

Use cases:

* Compliance requirements
* Bring Your Own License (BYOL)
* Isolation-sensitive workloads

Cheapest? ❌
Most expensive? ✔️

---

# 🌍 **8. Elastic IP**

Static public IPv4 address you can attach to an instance.

**Important:**
AWS charges for Elastic IP if it is **not attached** to a running instance.

Use cases:

* Stable IP for production server
* IP-based whitelisting

---

# 🔐 **9. Security Groups**

Virtual firewall for EC2.

Characteristics:

* Operates at **instance level**
* **Stateful** (return traffic automatically allowed)
* Only **allow rules**

Common rules:

* Allow SSH (22)
* Allow HTTP (80)
* Allow HTTPS (443)

---

# 🧭 **10. Placement Groups**

Placement groups control how EC2 instances are placed across hardware.

## **1️⃣ Cluster Placement Group**

Instances sit close together → **low latency, high throughput**.
Use case: HPC, big data.

## **2️⃣ Spread Placement Group**

Instances placed apart on different racks.
Use case: critical apps requiring HA.

## **3️⃣ Partition Placement Group**

Instances divided into partitions.
Use case: HDFS, Cassandra, Kafka clusters.

---




