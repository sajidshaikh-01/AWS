# Amazon RDS & SQL – Complete README

This README includes detailed explanations of:

* What is **Amazon RDS**
* **RDS engine types**
* **Basics of SQL**
* How to **connect a server/application to a database**
* **Read Replica** in RDS
* **Multi-AZ Deployment** in RDS
* **RDS Proxy**
* **Amazon Aurora**
* **Aurora Endpoints** (Writer, Reader, Instance, Custom)
* **Cross-Region Read Replica**
* **Interview Questions & Answers**

---

## 1. What is Amazon RDS?

Amazon RDS (**Relational Database Service**) is a fully managed AWS service that makes it easy to set up, operate, and scale relational databases.

AWS manages:

* Hardware provisioning
* OS installation and patching
* Database installation and patching
* Backups and snapshots
* Automatic failover (Multi-AZ)
* Monitoring and alerting

You manage only:

* Schema
* Data
* Queries
* Indexing
* Application logic

RDS reduces operational overhead and improves reliability and scalability.

---

## 2. Amazon RDS Database Engine Types

RDS supports 6 major database engines:

### **1. MySQL**

* Popular open-source database
* Works for web/WebApp workloads

### **2. PostgreSQL**

* Highly advanced open-source database
* Supports JSON, advanced indexing, and high performance

### **3. MariaDB**

* MySQL-compatible alternative
* Faster performance in certain cases

### **4. Oracle**

* Enterprise workloads requiring Oracle compatibility and features

### **5. Microsoft SQL Server**

* Used for enterprise and .NET-based applications

### **6. Amazon Aurora (MySQL & PostgreSQL compatible)**

* Cloud-native distributed storage
* 5x faster than MySQL and 3x faster than PostgreSQL
* Highly available and scalable

---

## 3. Basics of SQL

SQL (**Structured Query Language**) is used to interact with relational databases.

### **Common SQL Commands**

#### **DDL (Data Definition Language)**

```sql
CREATE TABLE users (id INT, name VARCHAR(50));
ALTER TABLE users ADD email VARCHAR(100);
DROP TABLE users;
```

#### **DML (Data Manipulation Language)**

```sql
INSERT INTO users VALUES (1, 'John');
UPDATE users SET name = 'Adam' WHERE id = 1;
DELETE FROM users WHERE id = 1;
```

#### **DQL (Data Query Language)**

```sql
SELECT * FROM users;
SELECT name FROM users WHERE id = 1;
```

#### **DCL (Data Control Language)**

```sql
GRANT SELECT ON users TO 'app_user';
REVOKE SELECT ON users FROM 'app_user';
```

---

## 4. How to Connect a Server/Application to an RDS Database

To connect, you need:

* RDS **Endpoint**
* **Port** (MySQL: 3306, PostgreSQL: 5432)
* **Username / Password**
* **Security group rules** allowing inbound traffic

### Example connection string

#### MySQL (Linux server)

```bash
mysql -h mydb.abcdef1234.us-east-1.rds.amazonaws.com -u admin -p
```

#### PostgreSQL

```bash
psql -h mydb.abcdef1234.us-east-1.rds.amazonaws.com -U admin -d mydb
```

### Application connection example (Python)

```python
import pymysql
conn = pymysql.connect(
    host='mydb.abcdef1234.us-east-1.rds.amazonaws.com',
    user='admin',
    password='password',
    db='mydb'
)
```

---

## 5. What is a Read Replica in RDS?

A **Read Replica** is a read-only copy of your primary database.

Used for:

* Reducing load on primary DB
* Scaling read-heavy applications
* Analytics and reporting
* Disaster recovery

### Features:

* Asynchronous replication
* Read-only endpoint
* Promotable to standalone DB

---

## 6. What is Multi-AZ in RDS?

Multi-AZ provides **high availability** by creating a synchronous standby replica in another Availability Zone.

### How it works:

* Primary DB → synchronously replicated to standby DB
* Automatic failover if primary fails

### Benefits:

* Zero data loss
* Automatic failover
* Ideal for production workloads

Note: Multi-AZ ≠ Read Replica (different use cases).

---

## 7. What is RDS Proxy?

RDS Proxy is a **connection pooling service** used with RDS and Aurora.

### Benefits:

* Improves application scalability
* Reduces DB connection overhead
* Speeds up failover
* Protects databases from sudden traffic spikes

### Uses:

* Serverless apps (Lambda)
* Microservices
* High-traffic APIs

---

## 8. What is Amazon Aurora?

Amazon Aurora is a cloud-native database built by AWS.

### Key Features:

* Compatible with MySQL and PostgreSQL
* Distributed storage across 6 replicas and 3 Availability Zones
* Auto-scaling read replicas
* Fast failover
* High performance

### Aurora Cluster Components:

* **Writer instance** (read/write)
* **Reader instances** (read-only)
* Shared storage volume

---

## 9. Aurora Endpoints

Aurora uses different endpoints for different purposes.

### **1. Writer Endpoint**

* Points to the primary (writer) instance
* Used for writes and reads

### **2. Reader Endpoint**

* Load balances across all read replicas
* Used for read-heavy workloads

### **3. Instance Endpoint**

* Connect directly to a specific instance
* Useful for diagnostics

### **4. Custom Endpoint**

* Allows grouping specific reader instances
* Used for workload separation (analytics vs API traffic)

---

## 10. Cross-Region Read Replica

Cross-Region Replicas replicate data from your primary DB to another region.

### Use Cases:

* Disaster recovery
* Global applications
* Data locality (serve users in other countries)

### Features:

* Asynchronous replication
* Can be promoted to standalone database
* Helps meet compliance requirements

---

# Interview Questions & Answers

### **1. What is Amazon RDS?**

A fully managed database service that handles provisioning, patching, backups, and recovery for relational databases.

---

### **2. What is the difference between Read Replica and Multi-AZ?**

| Read Replica             | Multi-AZ                   |
| ------------------------ | -------------------------- |
| Asynchronous replication | Synchronous replication    |
| Used to scale reads      | Used for high availability |
| Read-only                | Read/write failover        |
| No automatic failover    | Automatic failover         |

---

### **3. What is Aurora and why is it faster?**

Aurora is a cloud-native distributed database with shared storage, reducing metadata overhead and improving performance.

---

### **4. What is RDS Proxy used for?**

To manage and pool database connections, reduce overhead, and improve failover performance.

---

### **5. What are Aurora Endpoints?**

* Writer – for read/write
* Reader – load-balanced read-only
* Instance – direct instance access
* Custom – user-defined groups of readers

---

### **6. What is Cross-Region Read Replica?**

A read replica located in another AWS region for DR and global workloads.

---

### **7. How does application connect to RDS?**

Using the RDS endpoint + port + username/password and allowing traffic via security groups.

---

### **8. What is automatic failover in Multi-AZ?**

When primary DB fails, traffic automatically shifts to the standby instance.

---

### **9. What is SQL used for?**

To create, query, update, and manage relational database data.

---

### **10. When should we use Aurora instead of RDS MySQL?**

* High performance workloads
* Large-scale read-heavy apps
* Need multi-region DR
* Fast failover requirements

---

