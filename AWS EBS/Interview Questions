# 🧠 EBS Interview Questions & Answers

## **Q1: What is EBS?**

EBS is block storage for EC2. Persistent, scalable, and replicated within an AZ.

---

## **Q2: Difference between EBS and Instance Store?**

| EBS                     | Instance Store    |
| ----------------------- | ----------------- |
| Persistent              | Ephemeral         |
| Can stop/start instance | Data lost on stop |
| Snapshots supported     | No snapshots      |

---

## **Q3: Can you attach one EBS volume to multiple EC2 instances?**

Only with **EBS Multi-Attach** (supported on io1/io2).

---

## **Q4: What is Multi-Attach?**

Allows multiple EC2 instances in same AZ to access one EBS volume.

---

## **Q5: How to check disk size in EC2?**

```
lsblk
```

---

## **Q6: What is EBS Snapshot?**

A point-in-time backup stored in S3.

---

## **Q7: Can you restore a snapshot to a different region?**

Yes, snapshots can be copied cross-region.

---

## **Q8: What is the difference between gp3 and gp2?**

| gp3                        | gp2                      |
| -------------------------- | ------------------------ |
| Cheaper                    | More expensive           |
| Separate IOPS & throughput | IOPS tied to volume size |

---

## **Q9: What happens if you detach a volume without unmounting?**

Filesystem may get **corrupted**.

---

## **Q10: How to increase root volume size?**

1. Modify volume in console
2. Grow partition
3. Extend filesystem

---

## **Q11: How do you encrypt an EBS volume?**

Either:

* Enable encryption during creation
* Copy snapshot → create encrypted volume

---

## **Q12: Can you decrease EBS volume size?**

❌ No. Only increase.

---

## **Q13: How to list all EBS volumes using CLI?**

```
aws ec2 describe-volumes
```

---

## **Q14: What is the maximum EBS volume size?**

Up to **64 TiB**.

---

## **Q15: Does EBS support burst performance?**

Yes, **gp3**, **st1**, **sc1**, and **io2** support burst capabilities.

---
