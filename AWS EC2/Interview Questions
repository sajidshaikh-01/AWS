# 📝 EC2 Interview Questions & Answers

## **Q1. What is an EC2 Instance?**

A virtual server in AWS used to run applications.

---

## **Q2. Difference between stopping and terminating an instance?**

* **Stop** → Instance shuts down; EBS volumes remain.
* **Terminate** → Instance + EBS (if delete-on-termination=true) deleted.

---

## **Q3. What are the different EC2 instance types?**

General, Compute Optimized, Memory Optimized, GPU, Storage Optimized.

---

## **Q4. What is a Security Group?**

Instance-level firewall that controls inbound/outbound traffic.

---

## **Q5. Difference between Security Group and NACL?**

| Security Group   | NACL               |
| ---------------- | ------------------ |
| Stateful         | Stateless          |
| Instance level   | Subnet level       |
| Allow rules only | Allow + Deny rules |

---

## **Q6. What are Spot Instances?**

Unused EC2 capacity available at massive discounts but can be interrupted.

---

## **Q7. What are Reserved Instances?**

Discounted EC2 pricing when committing for 1 or 3 years.

---

## **Q8. What are Savings Plans?**

Flexible pricing model where you commit to a dollar-per-hour usage.

---

## **Q9. What is a Dedicated Host?**

A physical machine fully dedicated to your AWS account.

---

## **Q10. What is an Elastic IP?**

A static public IPv4 address that can be moved between instances.

---

## **Q11. What is a Placement Group?**

Controls hardware placement of instances—Cluster, Spread, and Partition.

---

## **Q12. What is an AMI?**

A template for launching EC2 instances containing OS + configuration.

---

## **Q13. What is User Data in EC2?**

Script executed when instance launches (for automation).

---

## **Q14. What is Instance Metadata?**

Info about the instance.

```
curl http://169.254.169.254/latest/meta-data/
```

---

## **Q15. How does Auto Scaling work with EC2?**

Automatically increases/decreases EC2 instances based on demand using ASG.

---

## **Q16. What is EBS and types?**

Block storage for EC2.
Types:

* gp3 (general)
* io1/io2 (high IOPS)
* sc1 / st1 (HDD)

---

## **Q17. Can one Elastic IP be assigned to multiple EC2 instances?**

No. It can be remapped but attached to only one at a time.

---

## **Q18. What is the maximum number of Elastic IPs per region?**

5 (can request more from AWS).

---

## **Q19. What happens when AWS interrupts a Spot Instance?**

You get a **2-minute warning** before shutdown.

---

## **Q20. Can we resize an EC2 instance?**

Yes. Stop instance → change instance type → start.

---
