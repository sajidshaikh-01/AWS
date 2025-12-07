# AWS VPC – IP Addressing, Private & Public IPs, CIDR Notation (Complete README)

This README explains **Private IP, Public IP, Elastic IP, CIDR ranges, Subnets, and IP addressing rules in AWS VPC**. Perfect for VPC fundamentals.

---

# 🌐 What is an IP Address?

An IP address identifies a device on a network.
Two major types:

* **Private IP** (internal communication)
* **Public IP** (internet communication)

AWS VPC supports both.

---

# 🏠 Private IP Address (Internal IP)

Private IP addresses are used for communication **within the VPC**.

### Features:

* Not accessible from the internet
* Free of cost
* Assigned automatically when an EC2 instance starts
* Stays with the instance until it's stopped (unless manually assigned)

### Private IP Ranges (RFC 1918):

AWS allows these private ranges:

* **10.0.0.0 – 10.255.255.255** (10/8)
* **172.16.0.0 – 172.31.255.255** (172.16/12)
* **192.168.0.0 – 192.168.255.255** (192.168/16)

Example:

```
10.0.1.25
172.31.10.5
192.168.100.10
```

Used for:

* EC2 internal communication
* Databases
* Backend services

---

# 🌍 Public IP Address

A public IP is **reachable from the internet**.

### Features:

* Assigned when launching EC2 in a **public subnet** with Auto-assign Public IP = YES
* Changes when instance is stopped & started
* NOT constant

Used for:

* Bastion hosts
* Web servers
* NAT instances (legacy)

---

# 🌟 Elastic IP (Static Public IP)

Elastic IP (EIP) is a **static** public IPv4 address.

### Features:

* Does NOT change after stop/start
* You can detach and attach to different instances
* AWS charges if not attached to a running instance

Use cases:

* Production servers
* Whitelisted access
* VPN endpoints

---

# 🧱 CIDR Notation (Defining IP Ranges)

CIDR = Classless Inter-Domain Routing
Used to define IP address ranges for VPC & Subnets.

Format:

```
IP_address/Prefix
```

Example:

```
10.0.0.0/16
```

Means:

* Prefix /16 → First 16 bits are network portion
* Total IPs = 65,536

### 📌 Common Prefix Sizes:

| CIDR | IP Count | Useful IPs | Usage         |
| ---- | -------- | ---------- | ------------- |
| /16  | 65,536   | 65,531     | Large VPC     |
| /20  | 4,096    | 4,091      | Medium subnet |
| /24  | 256      | 251        | Small subnet  |

AWS reserves **5 IPs** in every subnet:

* Network address (.0)
* VPC router (.1)
* AWS DNS (.2)
* Reserved future (.3)
* Broadcast (last IP)

Example: Subnet 10.0.1.0/24
Reserved IPs:

```
10.0.1.0
10.0.1.1
10.0.1.2
10.0.1.3
10.0.1.255
```

---

# 🧭 Public Subnet vs Private Subnet

### **Public Subnet**

Has **Internet Gateway** route.

```
0.0.0.0/0 → igw-12345
```

Instances receive **public IP**.

### **Private Subnet**

No direct internet route.

```
0.0.0.0/0 → nat-gateway-id
```

Instances only have **private IPs**.

---

# 🛠 How AWS Assigns IPs

## When launching an EC2 in a public subnet:

* Private IP = mandatory
* Public IP = optional
* Elastic IP = manual assignment

## When launching in a private subnet:

* Only private IP assigned
* Public IP = NO
* Internet access requires NAT Gateway

---


