# AWS EBS (Elastic Block Store) – Complete README
---
# 📦 What is Amazon EBS?

Amazon EBS (Elastic Block Store) provides **block-level storage** for EC2 instances.

### Key Features:

* Persistent storage (data survives EC2 stop/start)
* Highly available within an AZ
* Snapshots stored in S3
* Attach to 1 instance at a time (except Multi-Attach)

Used for:

* Databases
* Containers
* Operating systems
* High-performance apps

---

# 🔗 Attaching an EBS Volume

### Step 1: Create a volume

* Go to **EC2 Console → Elastic Block Store → Volumes → Create Volume**
* Choose AZ same as EC2 instance

### Step 2: Attach volume to EC2

* Select volume → **Actions → Attach Volume**
* Choose instance
* Example device name: `/dev/xvdf`

### Step 3: Format & mount volume

```
sudo mkfs -t xfs /dev/xvdf
sudo mkdir /data
sudo mount /dev/xvdf /data
```

### Step 4: Make mount permanent

Add to `/etc/fstab`:

```
/dev/xvdf /data xfs defaults 0 0
```

---

# 🔌 Detaching an EBS Volume

### Step 1: Unmount

```
sudo umount /data
```

### Step 2: Detach from console

* EC2 Console → Volumes → Select Volume → **Detach Volume**

### WARNING

❌ Never detach without unmounting → filesystem corruption possible.

---

# 📈 Resize (Expand) EBS Volume

EBS supports **online expansion** (root and non-root volumes).

### Step 1: Modify size

* Go to **Volumes → Modify Volume**
* Increase size

### Step 2: Check if OS detected new size

```
lsblk
```

### Step 3: Extend filesystem

#### For EXT4:

```
sudo resize2fs /dev/xvdf
```

#### For XFS:

```
sudo xfs_growfs -d /
```

---

# 🔧 Resize the Root EBS Volume

When EC2 root disk is full, resize like this:

### Step 1: Modify root volume in AWS console

* Volumes → Select root volume → **Modify Volume**

### Step 2: On instance, verify

```
lsblk
```

### Step 3: Grow partition (if needed)

```
sudo growpart /dev/xvda 1
```

### Step 4: Resize filesystem

#### EXT4:

```
sudo resize2fs /dev/xvda1
```

#### XFS:

```
sudo xfs_growfs -d /
```

---

# 📚 Types of EBS Volumes

AWS offers 5 main types:

| Type                  | Description              | Use Case                      |
| --------------------- | ------------------------ | ----------------------------- |
| **gp3**               | General-purpose SSD      | Most workloads                |
| **gp2**               | Older SSD type           | Legacy apps                   |
| **io1/io2**           | Provisioned IOPS SSD     | Databases, high IOPS          |
| **st1**               | HDD Throughput optimized | Big data, logs                |
| **sc1**               | Cold HDD                 | Low-cost rarely accessed data |
| **io2 Block Express** | Highest performance      | Enterprise workloads          |

### Summary:

* **SSD** → gp3, gp2, io1, io2
* **HDD** → st1, sc1

---



