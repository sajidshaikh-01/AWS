# AWS EBS Snapshots – Complete README
---
# 📸 What is an EBS Snapshot?

An **EBS Snapshot** is a point-in-time backup of an Amazon EBS volume.

### Key Features:

* Stored in **Amazon S3** (managed by AWS)
* **Incremental** backups (only changed blocks saved)
* Can be used to create new EBS volumes
* Supports **cross-region** and **cross-account** copy
* Good for backups, DR, automation

Snapshots are **region-specific** but can be copied.

---

# 🧠 How EBS Snapshots Work

* First snapshot = full backup
* Next snapshots = incremental changes only
* Restoring a snapshot creates a new EBS volume

AWS handles deduplication and block-level storage.

---

# 🛠️ How to Create a Snapshot

### Option 1: From EC2 Console

1. Open **EC2 Console → Volumes**
2. Select volume
3. **Actions → Create Snapshot**
4. Add description & tags

### Option 2: CLI

```
aws ec2 create-snapshot --volume-id vol-123456 --description "Daily backup"
```

---

# 🔁 How to Restore a Snapshot

### Create a new EBS volume from snapshot:

1. EC2 Console → **Snapshots**
2. Select snapshot
3. **Actions → Create Volume**
4. Attach volume to EC2

CLI:

```
aws ec2 create-volume --snapshot-id snap-12345 --availability-zone ap-south-1a
```

---

# 🌍 Copy Snapshot to Another Region

Used for disaster recovery.

### Console:

Snapshots → Select snapshot → **Copy Snapshot**

### CLI:

```
aws ec2 copy-snapshot --source-region ap-south-1 --source-snapshot-id snap-123 --destination-region us-east-1
```

---

# 🔐 Cross-Account Snapshot Sharing

You can share snapshots with another AWS account.

Steps:

* Select snapshot
* Modify **permissions** to allow target AWS Account ID

Constraints:

* Only **un-encrypted** snapshots can be shared directly
* Encrypted snapshots require sharing the KMS key

---

# 🔄 Automated Snapshots with Lifecycle Policies

Use **Amazon Data Lifecycle Manager (DLM)** to automate:

* Daily snapshots
* Weekly snapshots
* Retention policies

### Create a Policy:

1. Open EC2 → **Lifecycle Manager**
2. Create Policy
3. Select volumes or tags
4. Configure schedule
5. Define retention (e.g., keep 7 days)

---

# 🔧 Delete a Snapshot

Console:

* EC2 → Snapshots → Select → **Delete**

CLI:

```
aws ec2 delete-snapshot --snapshot-id snap-12345
```

---

# 🧹 Snapshot Storage & Costs

### You pay for:

* Total size stored (after incremental compression)
* Copies (cross-region copies cost double)
* Fast Snapshot Restore (FSR) if enabled

### You do NOT pay for:

* Snapshots that contain duplicate blocks

---

# ⚡ Fast Snapshot Restore (FSR)

FSR makes restored volumes perform at full speed immediately.

Enable:

```
aws ec2 enable-fast-snapshot-restores --availability-zones ap-south-1a --source-snapshot-id snap-12345
```

Cost: Extra charges apply.

---

# 🎯 Snapshot Best Practices

* Tag snapshots with project, environment, owner
* Automate with DLM
* Copy snapshots cross-region for DR
* Encrypt snapshots for security
* Delete unused snapshots to reduce cost

---



