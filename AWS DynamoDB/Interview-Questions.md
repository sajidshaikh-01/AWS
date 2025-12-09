# Interview Questions & Answers

### **1. What is DynamoDB?**

A fully managed, serverless NoSQL key-value/document database offering millisecond performance.

---

### **2. Difference between Partition Key and Sort Key?**

* Partition Key → determines partition placement.
* Sort Key → allows multiple items in the same partition, ordered by SK.

---

### **3. When do you use Query vs Scan?**

* **Query** → efficient, uses keys, fast.
* **Scan** → scans full table, slow, expensive.

---

### **4. What is a GSI?**

A secondary index with different PK/SK, allowing new query patterns.

---

### **5. What is LSI? How is it different from GSI?**

* LSI → Same PK, different SK, created at table creation.
* GSI → Different PK/SK, can be added anytime.

---

### **6. What is WCU/RCU?**

Defines provisioned read/write throughput.

---

### **7. What is PITR?**

Point-in-time recovery allowing restore to any second in last 35 days.

---

### **8. What are DynamoDB Global Tables?**

Multi-region replicated tables for global applications.

---

### **9. How do you export DynamoDB data to S3?**

Using Export to S3 feature without consuming RCU.

---

### **10. How does DynamoDB ensure high availability?**

Multi-AZ replication within a region and optional multi-region global tables.

---

