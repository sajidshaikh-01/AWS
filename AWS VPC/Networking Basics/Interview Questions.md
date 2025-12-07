# 🧠 Interview Questions & Answers

## **Q1: What is the difference between a public and private IP?**

**Private IP** → Used for internal communication inside VPC.
**Public IP** → Used to access internet.

---

## **Q2: What is an Elastic IP?**

A static public IPv4 address that does not change after restarting an EC2 instance.

---

## **Q3: Can private IPs communicate with the internet?**

Only via **NAT Gateway** or **NAT Instance**.

---

## **Q4: How many IPs does AWS reserve in each subnet?**

**5 IPs**.

---

## **Q5: What does /24 mean in CIDR?**

A subnet with **256 total IPs**, 251 usable.

---

## **Q6: Which private IP ranges does AWS allow?**

10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16.

---

## **Q7: What is the difference between Public Subnet and Private Subnet?**

* **Public:** Route to IGW, public IP available.
* **Private:** No IGW route, no public IP.

---

## **Q8: What happens to public IP when EC2 is stopped?**

It is **released**.

---

## **Q9: Does Elastic IP change after reboot?**

No.

---

## **Q10: Can I attach Elastic IP to EC2 in private subnet?**

Yes, but instance will still not have internet unless subnet has IGW route.

---

## **Q11: What is the maximum VPC size?**

/16 (65,536 IPs).

---

## **Q12: Can we change the VPC CIDR after creation?**

Yes, you can **add** new CIDRs but cannot shrink existing one.

---
