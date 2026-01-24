# 🌐 AWS Route 53 – 

---

## 1️⃣ What is Route 53?

**AWS Route 53** is a **managed DNS (Domain Name System) service** provided by AWS.

**Simple definition:**

> Route 53 translates **domain names into IP addresses** and routes user traffic to the correct AWS resources.

Example:

```
www.example.com → 54.10.20.30
```

---

## 2️⃣ Why is it called Route 53?

* **Route** → Routes traffic
* **53** → DNS uses **port 53**

---

## 3️⃣ What Problems Does Route 53 Solve?

* Converts domain name → IP address
* Routes traffic to nearest / healthy resources
* Improves availability and performance
* Integrates deeply with AWS services

---

## 4️⃣ Route 53 Core Components

### 🔹 Domain Registration

* Buy and manage domains

### 🔹 Hosted Zones

* Container for DNS records

Types:

* **Public Hosted Zone** → Internet-facing domains
* **Private Hosted Zone** → Internal AWS (VPC-only)

---

## 5️⃣ Route 53 Record Types (VERY IMPORTANT)

### 🔸 A Record (MOST USED)

Maps a domain name to an **IPv4 address**.

Example:

```
example.com → 54.10.20.30
```

---

### 🔸 AAAA Record

Maps a domain name to an **IPv6 address**.

---

### 🔸 CNAME Record

Maps one domain name to **another domain name**.

Example:

```
www.example.com → example.com
```

⚠️ Cannot be used for root domain.

---

### 🔸 Alias Record (AWS-SPECIFIC – INTERVIEW FAVORITE)

Points a domain to AWS resources:

* ALB
* CloudFront
* S3

Example:

```
example.com → ALB
```

✅ Works with root domain

---

### 🔸 MX Record

Used for **email routing**.

Example:

```
Mail server → Google Workspace
```

---

### 🔸 TXT Record

Stores **text values**.

Used for:

* Domain verification
* SPF / DKIM (email security)

---

### 🔸 NS Record

Specifies **name servers** for the domain.

Automatically created with hosted zones.

---

## 6️⃣ Route 53 Routing Policy Types (EXTREMELY IMPORTANT)

Routing policies decide **how traffic is routed** when multiple records exist.

---

### 1️⃣ Simple Routing Policy

* Single resource
* No health checks

Use case:

```
One website → one server
```

---

### 2️⃣ Weighted Routing Policy

* Split traffic by percentage

Example:

```
Version A → 70%
Version B → 30%
```

Use case:

* Canary deployments
* A/B testing

---

### 3️⃣ Latency-Based Routing Policy

* Routes traffic to **lowest latency region**

Use case:

* Global applications

---

### 4️⃣ Failover Routing Policy (VERY COMMON)

* Primary + Secondary
* Uses health checks

Use case:

```
Primary down → route to backup
```

---

### 5️⃣ Geolocation Routing Policy

* Routes traffic based on **user location**

Use case:

* Country-specific content

---

### 6️⃣ Geoproximity Routing Policy

* Routes traffic based on **distance to resources**

Use case:

* Traffic shifting between regions

---

### 7️⃣ Multi-Value Answer Routing

* Returns multiple healthy IPs

Use case:

* Simple load balancing

---

## 7️⃣ Route 53 Health Checks

* Checks endpoint health
* Integrates with Failover & Multi-value routing

Health check methods:

* HTTP
* HTTPS
* TCP

---

## 8️⃣ Real DevOps Architecture Example

```
User → Route 53 → ALB → EC2 / EKS
```

If ALB fails → Route 53 routes to backup region.

---

## 9️⃣ Common Interview Questions (Quick Prep)

### ❓ Alias vs CNAME?

* Alias → AWS resources, root domain supported
* CNAME → Domain to domain only

---

### ❓ Route 53 vs Load Balancer?

* Route 53 → DNS level routing
* Load Balancer → Application traffic routing

---


🚀 **This README is beginner-friendly, DevOps-focused, and interview-ready.**

