# AWS Auto Scaling Groups (ASG) – Complete README

This README covers **Auto Scaling Groups**, Launch Templates, Scaling Policies, Lifecycle Hooks, Load Balancer integration, Health Checks, and Interview Questions with Answers.
Perfect for DevOps, AWS Solutions Architect, and Cloud Engineer preparation.

---

# 🚀 What is an Auto Scaling Group (ASG)?

An Auto Scaling Group automatically **adds or removes EC2 instances** based on demand, ensuring:

* High availability
* Fault tolerance
* Cost optimization

ASG maintains the **desired number of instances** at all times.

Example:
If desired capacity = 3 and one EC2 fails → ASG launches a new one.

---

# 🧱 Components of Auto Scaling

## 1️⃣ **Launch Template**

A template containing EC2 configuration:

* AMI
* Instance type
* Security groups
* EBS volumes
* Key pair
* User data scripts

ASG uses Launch Templates to create new EC2 instances.

---

## 2️⃣ **Auto Scaling Group (ASG)**

Defines:

* Minimum capacity
* Maximum capacity
* Desired capacity
* Subnets
* Health check type
* Load balancer/target group

Example:

```
Min = 2
Desired = 3
Max = 5
```

---

## 3️⃣ **Scaling Policies**

Scaling policies decide **when** to scale in/out.

### Types:

### 🔹 Target Tracking Policy (Recommended)

Maintains a specific metric target.
Example:

* CPU at 50%
* ALB request count

### 🔹 Step Scaling

Scales in/out in steps.
Example:

* CPU > 60% → add 1 instance
* CPU > 80% → add 2 instances

### 🔹 Simple Scaling

Older method; add/remove instances after cooldown.

---

# 📊 Common Metrics Used for Scaling

* CPU Utilization
* Memory (with CloudWatch agent)
* ALB RequestCountPerTarget
* NetworkIn / NetworkOut
* Custom CloudWatch metrics

---

# 🩺 Health Checks

ASG supports two types:

* **EC2 health checks**
* **ELB health checks**

If an instance fails health checks → ASG terminates and replaces it.

---

# 🌐 ASG + Load Balancer Integration

ASG integrates with:

* Application Load Balancer
* Network Load Balancer

ASG automatically registers & deregisters instances from Target Groups.

---

# 🔄 Lifecycle Hooks

Lifecycle hooks control instance launch/termination.

Examples:

* Run configuration scripts before instance becomes “InService”
* Drain connections before termination

Use SNS or SQS to trigger automation.

---

# 🔁 Cooldown Period

Cooldown prevents rapid scaling actions.
Default cooldown = 300 seconds.

---

# 🏷️ Instance Refresh

ASG can replace instances automatically when:

* Launch template changes
* AMI updates
* Security patches needed

---

# 🔐 Predictive Scaling

Uses machine learning to predict traffic patterns.
Available with:

* ASG + CloudWatch

---

# 🧪 Auto Scaling CLI Commands

### Create an ASG:

```
aws autoscaling create-auto-scaling-group \
 --auto-scaling-group-name myASG \
 --launch-template LaunchTemplateName=mytemplate \
 --min-size 1 --max-size 5 --desired-capacity 2 \
 --vpc-zone-identifier subnet-123,subnet-456
```

### Attach to Load Balancer:

```
aws autoscaling attach-load-balancer-target-groups \
 --auto-scaling-group-name myASG \
 --target-group-arns arn:aws:elasticloadbalancing:...
```





