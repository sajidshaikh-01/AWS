# AWS Basics – Cloud Computing & Global Infrastructure (README)

This README provides a clean, beginner‑friendly explanation of **Cloud Computing** and **AWS Global Infrastructure**, 

---

# 🌥️ **What is Cloud Computing?**

Cloud computing is the on‑demand delivery of IT resources over the internet with **pay‑as‑you‑go** pricing.

## ✅ **Key Characteristics of Cloud Computing**

### **1. On‑Demand Resources**

You can provision servers, databases, and storage whenever needed — without manual hardware setup.

### **2. Pay‑As‑You‑Go**

You pay only for what you use. No upfront hardware cost.

### **3. Scalability**

Resources automatically scale **up or down** based on demand.

### **4. High Availability**

Cloud infrastructure ensures minimal downtime using:

* Multi‑region deployment
* Load balancing
* Automatic failover

### **5. Security**

AWS provides encryption, IAM policies, network isolation, and compliance features.

### **6. Global Reach**

Deploy applications across the world using AWS Regions.

---

# 🌍 **AWS Global Infrastructure**

AWS has a globally distributed architecture designed for speed, reliability, and resilience.

## **Components of AWS Global Infrastructure:**

### 🔹 **1. Regions**

A region is a geographical area.

* Each region has multiple isolated Availability Zones.
* Example: `us-east-1`, `ap-south-1`.

Use cases:

* Deploying resources close to users
* Storing data for compliance (e.g., India region for Indian customer data)

---

### 🔹 **2. Availability Zones (AZs)**

An AZ is one or more data centers with independent power, cooling, and networking.

* Each region has **≥ 2 AZs**.
* High availability is achieved by deploying across multiple AZs.

Example:
`ap-south-1a`, `ap-south-1b`, `ap-south-1c`

---

### 🔹 **3. Edge Locations**

Locations where AWS caches data **closer to end users**.

* Used by **Amazon CloudFront (CDN)**.
* Improves website speed globally.

Example: Edge locations in Mumbai, Delhi, Bangalore.

---

## 📌 Summary

Cloud computing provides:

* On‑demand resources
* Pay‑as‑you‑go pricing
* Scalability
* High availability

AWS Global Infrastructure is built using:

* Regions
* Availability Zones
* Edge Locations

Together, they provide a highly reliable and globally distributed cloud platform.

---

