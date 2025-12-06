# 🧠 EBS Snapshot Interview Questions & Answers

## **Q1: What is an EBS Snapshot?**

A point-in-time, incremental backup of an EBS volume stored in S3.

---

## **Q2: Are snapshots incremental?**

Yes. Only changed blocks are stored after the first snapshot.

---

## **Q3: Can snapshots be copied to another region?**

Yes. This is used for **disaster recovery**.

---

## **Q4: How do you restore a snapshot?**

Create a new EBS volume from the snapshot and attach it to EC2.

---

## **Q5: Difference between snapshot and AMI?**

| Snapshot             | AMI                      |
| -------------------- | ------------------------ |
| Backup of EBS volume | Full machine image       |
| Cannot boot alone    | Can launch EC2 instances |

---

## **Q6: Can you share snapshots with another AWS account?**

Yes.

* Unencrypted snapshots → directly share
* Encrypted → must share KMS key

---

## **Q7: What is Fast Snapshot Restore (FSR)?**

Feature that lets restored volumes deliver full performance instantly.

---

## **Q8: Can you take a snapshot of a root volume while running?**

Yes. Snapshots are **crash-consistent**.

---

## **Q9: How to automate snapshot creation?**

Using **Amazon Data Lifecycle Manager (DLM)**.

---

## **Q10: Does deleting a volume delete its snapshots?**

No. Snapshots remain until manually deleted.

---
