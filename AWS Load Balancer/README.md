# AWS Elastic Load Balancer (ELB) – Complete README

This README covers **Elastic Load Balancer concepts**, all ELB types (ALB, NLB, CLB, GWLB), listeners, target groups, health checks, sticky sessions, cross-zone balancing, and interview questions with answers.
Perfect for AWS, DevOps, and SAA preparation.

---

# ⚖️ What is an Elastic Load Balancer (ELB)?

Elastic Load Balancer automatically distributes incoming traffic across multiple EC2 instances, containers, or IP addresses.

### ELB provides:

* High availability
* Fault tolerance
* Automatic scaling
* Health checks

---

# 🌐 Types of Load Balancers in AWS

AWS provides **four** types of load balancers:

---

## 🟦 1. Application Load Balancer (ALB)

Layer: **Layer 7 (HTTP/HTTPS)**

### Features:

* URL-based routing (path-based)
* Host-based routing
* Routing to multiple target groups
* WebSocket support
* Best for microservices
* Supports Lambda targets
* Supports authentication (OIDC, Cognito)

**Use cases:**

* Web applications
* API services
* Containers (ECS/EKS)

---

## 🟩 2. Network Load Balancer (NLB)

Layer: **Layer 4 (TCP/UDP/TLS)**

### Features:

* Ultra-high performance
* Millions of requests per second
* Static IP support
* Zonal failover

**Use cases:**

* Gaming servers
* Realtime apps
* Low-latency traffic
* Handling TCP-heavy workloads

---

## 🟧 3. Classic Load Balancer (CLB)

Layer: **Layer 4 & Layer 7** (Legacy)

### Features:

* Basic load balancing
* Not recommended for new applications
* Supports EC2-Classic (deprecated)

**Use cases:**

* Legacy workloads only

---

## 🟥 4. Gateway Load Balancer (GWLB)

Layer: **Layer 3 (Network Gateway)**

### Features:

* Deploy 3rd-party firewalls
* Intrusion detection systems (IDS)
* Intrusion prevention systems (IPS)
* Traffic inspection

**Use cases:**

* Security appliances
* Network inspection

---

# 🎯 Target Groups

Load balancers send traffic to **Target Groups**.
Targets can be:

* EC2 instances
* IP addresses
* Lambda functions
* ECS tasks

Each target group has:

* Port
* Protocol
* Health checks

---

# 🩺 Health Checks

ELB continuously checks backend health.

Example ALB health check:

```
Path: /health
Protocol: HTTP
Healthy threshold: 3
Unhealthy threshold: 2
Timeout: 5 sec
Interval: 30 sec
```

Only healthy targets receive traffic.

---

# 🔁 Load Balancer Listeners

A listener checks connection requests using a protocol and port.

Examples:

* ALB → port 80 (HTTP), 443 (HTTPS)
* NLB → TCP/UDP

---

# 🔒 SSL Termination

ALB/NLB can handle SSL/TLS certificates via **ACM**.

This reduces CPU load on EC2 instances.

---

# 🧲 Sticky Sessions (Session Affinity)

Sticky sessions ensure the same user is routed to the same backend server.

Available in:

* ALB (application-based cookies)
* CLB (load balancer cookies)

Not available in NLB.

---

# 🌍 Cross-Zone Load Balancing

Distributes traffic evenly across all AZs.

* **ALB:** Always enabled (free)
* **NLB:** Optional (may incur cost)
* **CLB:** Optional

---

# 📈 ELB Scaling

Load balancers automatically scale:

* Request rate
* Network traffic
* Backend capacity

No manual intervention needed.

---

# 🔧 Access Logs

ELB can store logs in S3 to analyze:

* Client IP
* Latency
* Backend response
* User behavior

---

# 🛠️ Common ELB Use Cases

* Web servers (ALB)
* APIs & microservices (ALB)
* High-throughput TCP apps (NLB)
* Security appliance traffic (GWLB)
* Legacy apps (CLB)

---


