# Amazon DynamoDB – Complete README

This README covers everything you need to understand and work with **Amazon DynamoDB**, including:

* What is DynamoDB
* Primary Keys & Attributes
* How to Create a Table
* Where DynamoDB is used
* Scan vs Query
* Read/Write Capacity Units
* Local Secondary Index (LSI)
* Global Secondary Index (GSI)
* Point-in-Time Recovery (PITR)
* Global Tables (Multi-Region Replication)
* Export DynamoDB data to S3
* Import DynamoDB data from S3
* Interview Questions & Answers

---

## 1. What is Amazon DynamoDB?

Amazon DynamoDB is a **fully managed NoSQL database** that provides:

* Single-digit millisecond performance
* Automatic scaling
* Serverless architecture
* Key-value & document data model

DynamoDB can handle millions of requests per second without managing servers.

---

## 2. Primary Keys in DynamoDB

Every DynamoDB table must have a **Primary Key**, which uniquely identifies each item.

### Two Types of Primary Keys:

### **1. Partition Key (PK)**

* A single attribute used to uniquely identify items.
* All items with the same PK go into the same partition.
* Example:

```json
{"userId": "123"}
```

### **2. Partition Key + Sort Key (Composite Key)**

* More flexible and efficient querying.
* Example:

```json
{"userId": "123", "orderId": "A001"}
```

* Allows multiple items with same PK but different SK.

---

## 3. Attributes in DynamoDB

Attributes = columns in relational DB.

Types:

* String
* Number
* Binary
* Boolean
* Null
* List
* Map
* Set (Number Set, String Set, Binary Set)

---

## 4. How to Create a Table in DynamoDB

### AWS Console:

1. Go to DynamoDB
2. Click **Create Table**
3. Provide table name
4. Choose primary key
5. Select capacity mode (On-demand or Provisioned)
6. Add indexes (LSI/GSI if needed)
7. Create

### AWS CLI Example:

```bash
aws dynamodb create-table \
  --table-name Users \
  --attribute-definitions AttributeName=userId,AttributeType=S \
  --key-schema AttributeName=userId,KeyType=HASH \
  --billing-mode PAY_PER_REQUEST
```

---

## 5. Where Am I Using DynamoDB?

DynamoDB is ideal for:

* Serverless applications
* High-traffic APIs
* Gaming leaderboards
* IoT device data storage
* E-commerce carts
* User profile storage
* Session management
* Real-time data analytics

---

## 6. Scan vs Query

### **Scan**

* Reads **every item** in the table.
* Slow and expensive.
* Use only when absolutely necessary.

### **Query**

* Retrieves items using **Primary Key** or **GSI/LSI**.
* Fast and recommended.
* Supports filters and Sort Key conditions.

**Always prefer Query over Scan.**

---

## 7. Read and Write Capacity Units (RCU/WCU)

### **RCU (Read Capacity Unit)**

1 RCU = 1 strongly consistent read/sec of 4KB OR 2 eventually consistent reads/sec.

### **WCU (Write Capacity Unit)**

1 WCU = 1 write/sec for 1KB item.

### Capacity Modes:

* **Provisioned** (you set RCU/WCU)
* **On-demand** (DynamoDB auto-scales)

---

## 8. Local Secondary Index (LSI)

LSI:

* Created only at table creation.
* Same **Partition Key** as the main table.
* Different **Sort Key**.
* Maximum of 5 LSIs.

Used for alternate **sort orders**.

Example:

* PK = userId
* SK = orderDate
* LSI = sort by amount

---

## 9. Global Secondary Index (GSI)

GSI:

* Can be created anytime.
* Different **Partition Key and Sort Key**.
* Offers flexible querying for large tables.

Example:

* Table PK = userId
* GSI PK = email

GSIs require **additional RCU/WCU**.

---

## 10. Point-in-Time Recovery (PITR)

PITR allows restoring the table to **any second in the last 35 days**.

Benefits:

* Protects against accidental writes/deletes
* Automatic continuous backup

---

## 11. Global Tables: Multi-Region Replication

DynamoDB Global Tables automatically replicate data across **multiple AWS regions**.

Benefits:

* Low-latency access for global users
* Multi-region failover
* Active-active architecture

---

## 12. Export DynamoDB Data to S3

Export is done **without consuming RCU**.

Using AWS Console:

1. Go to DynamoDB Table
2. Choose **Exports and streams**
3. Export to Amazon S3 in Parquet/JSON format

---

## 13. Import DynamoDB Data From S3

You can import large datasets from S3 into DynamoDB.

Steps:

1. Create file in S3 (JSON lines format)
2. Go to DynamoDB → Imports
3. Select S3 bucket & file
4. Choose table name
5. Import

Common Use Case → migration from RDS, MongoDB, or CSV files.

---

