# AWS CloudFormation – Complete Documentation

AWS CloudFormation is an **Infrastructure as Code (IaC)** service that helps you automate the provisioning and management of AWS resources using templates written in **YAML** or **JSON**.

This README provides:

* Overview
* Core concepts
* Template structure
* Sample templates
* Deployment methods
* Best practices
* Real-world use cases

---

## 📘 1. What Is AWS CloudFormation?

CloudFormation allows you to **model, create, update, and delete AWS resources automatically**.

You define resources in a template → CloudFormation provisions them as a **stack**.

Example resources:

* EC2 Instances
* VPCs & Subnets
* IAM Roles
* S3 Buckets
* Lambda Functions
* RDS Databases
* API Gateway

---

## 🧩 2. CloudFormation Core Concepts

### **1. Template**

Written in YAML or JSON. Contains:

* Parameters
* Mappings
* Conditions
* Resources
* Outputs

### **2. Stack**

A deployed set of resources created from a template.

### **3. Change Set**

Preview of changes before applying updates.

### **4. Drift Detection**

Detects manual changes made outside CloudFormation.

---

## 📄 3. CloudFormation Template Structure (YAML)

```yaml
AWSTemplateFormatVersion: "2010-09-09"
Description: Sample CloudFormation Template

Parameters:
  InstanceType:
    Type: String
    Default: t2.micro

Resources:
  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: !Ref InstanceType
      ImageId: ami-0c55b159cbfafe1f0

Outputs:
  InstanceId:
    Value: !Ref MyEC2Instance
```

---

## 🚀 4. Deploying a CloudFormation Stack

### Using AWS Management Console

1. Go to **CloudFormation Console**
2. Click **Create stack**
3. Upload template file
4. Provide parameters
5. Click **Create**

### Using AWS CLI

**Create stack**

```bash
aws cloudformation create-stack \
  --stack-name demo-stack \
  --template-body file://template.yaml \
  --parameters ParameterKey=InstanceType,ParameterValue=t2.micro
```

**Update stack**

```bash
aws cloudformation update-stack \
  --stack-name demo-stack \
  --template-body file://template.yaml
```

**Delete stack**

```bash
aws cloudformation delete-stack --stack-name demo-stack
```

---

## 📦 5. Example Templates

### **Example: S3 Bucket**

```yaml
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: my-demo-bucket-12345
```

---

### **Example: EC2 Instance with Security Group**

```yaml
Resources:
  WebSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Allow HTTP
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0

  WebServer:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro
      ImageId: ami-0c55b159cbfafe1f0
      SecurityGroupIds:
        - !Ref WebSecurityGroup
```

---

## 🛡 6. Best Practices

* Use **version control** for templates
* Always use **Change Sets** before updating production
* Use **Parameters** to make templates reusable
* Use **IAM roles** instead of inline policies
* Prefer **modular templates** using Nested Stacks
* Enable **termination protection** for important stacks

---

## 🛠 7. Real-World Use Cases

* Deploying complete VPC networks
* Automating EC2 clusters
* Building serverless apps (Lambda + API Gateway)
* Provisioning RDS, ElastiCache, DynamoDB
* CI/CD pipelines using CodePipeline + CodeBuild
* Multi-account AWS environments

---

## 📌 8. Folder Structure for GitHub

```
cloudformation-project/
│
├── templates/
│   ├── vpc.yaml
│   ├── ec2.yaml
│   ├── s3.yaml
│   ├── iam.yaml
│
├── examples/
│   ├── ec2-sample.yaml
│   ├── s3-sample.yaml
│
└── README.md
```

