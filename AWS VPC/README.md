# AWS VPC – Complete Networking README (VPC, Subnets, Routing, IGW, NAT, Peering, NACL, Transit Gateway, Endpoints, VPN + 50 Interview Questions)

This README provides a full understanding of **AWS VPC and networking**, including core components and scenario-based interview questions.

---

# 🌐 **1. What is a VPC (Virtual Private Cloud)?**

A VPC is a logically isolated virtual network in AWS where you can launch AWS resources like EC2, RDS, EKS, etc.

### Key features:

* Full control over IP addressing
* Subnets
* Routing
* Security (SG, NACL)
* Connectivity options (VPN, Direct Connect)

Default VPC exists automatically; custom VPC gives full control.

---

# 🧱 **2. Subnets & Types**

Subnets divide a VPC into smaller networks.
Each subnet exists in exactly **one Availability Zone**.

### **Types of Subnets:**

## **1️⃣ Public Subnet**

* Route table has a route to Internet Gateway.

```
0.0.0.0/0 → igw-xxxx
```

* Instances can have Public IP/Elastic IP.

## **2️⃣ Private Subnet**

* No route to Internet Gateway.
* Can reach internet through NAT Gateway.

```
0.0.0.0/0 → nat-gw-id
```

## **3️⃣ Isolated Subnet**

* No internet access
* No NAT access
* Used for: Databases, internal services.

---

# 🛣️ **3. Route Tables**

Routing tables determine how traffic flows inside/outside VPC.

### Contains:

* Destination (CIDR)
* Target (IGW, NAT, Local, TGW, VPC Peering)

### The LOCAL route:

Automatically present:

```
VPC CIDR → local
```

Allows communication inside VPC.

---

# 🌐 **4. Internet Gateway (IGW)**

A horizontally scaled component enabling internet access.

Public subnets must route traffic to IGW.

---

# 🔁 **5. NAT Gateway**

Allows **private subnet** instances to access the internet while staying unreachable from the internet.

### Key points:

* Managed service
* Placed in **public subnet**
* Elastic IP is required
* High availability within AZ

---

# 🔗 **6. VPC Peering**

Connects two VPCs privately.
Works within:

* Same region
* Cross-region
* Cross-account

### Limitations:

* No transitive peering
* CIDR blocks cannot overlap

Used for internal communication between apps in different VPCs.

---

# 🛡️ **7. Network ACL (NACL)**

A subnet-level firewall.

### Characteristics:

* Stateless
* Allows + Denies
* Rules evaluated in order

NACLs protect entire subnets.

---

# 🔒 **8. Security Group vs NACL**

| Feature    | Security Group      | NACL                 |
| ---------- | ------------------- | -------------------- |
| Level      | Instance            | Subnet               |
| Stateful   | Yes                 | No                   |
| Allow only | Yes                 | No (Allow + Deny)    |
| Evaluation | Applied immediately | Evaluated rule order |

---

# 🛣️ **9. Transit Gateway (TGW)**

A hub-and-spoke model for connecting:

* Multiple VPCs
* VPN connections
* On-prem networks

### Benefits:

* Supports transitive routing (unlike VPC peering)
* Scalable
* Multi-account support

---

# 🔌 **10. VPC Endpoints**

Endpoints allow private connections to AWS services **without using the internet**.

### **Two types:**

### **1️⃣ Interface Endpoint (ENI-based)**

Used for services like:

* SSM
* CloudWatch
* Secrets Manager

### **2️⃣ Gateway Endpoint**

Only for:

* S3
* DynamoDB

---

# 🔗 **11. Site-to-Site VPN**

A secure IPSec VPN tunnel between:

* On-premises datacenter
* AWS VPC

### Components:

* Virtual Private Gateway (VGW)
* Customer Gateway (CGW)

Used for hybrid cloud.

---


