## 📝 CloudFormation Interview Questions & Answers

### **1. What is AWS CloudFormation?**

CloudFormation is an Infrastructure-as-Code (IaC) service that automates provisioning and managing AWS resources using templates.

---

### **2. What are the main sections of a CloudFormation template?**

* **Parameters** – User inputs
* **Mappings** – Static key-value data
* **Conditions** – Logic-based creation
* **Resources** – AWS resources to create (mandatory)
* **Outputs** – Values returned after stack creation

---

### **3. What is a CloudFormation Stack?**

A collection of AWS resources created, updated, or deleted together using a template.

---

### **4. What is a Change Set?**

It allows you to preview the impact of template changes before applying them to a stack.

---

### **5. What is Drift Detection?**

A feature to detect **manual changes** made to stack resources outside CloudFormation.

---

### **6. Difference between CloudFormation vs Terraform?**

| CloudFormation                 | Terraform                       |
| ------------------------------ | ------------------------------- |
| AWS-only                       | Multi-cloud                     |
| YAML/JSON                      | HCL                             |
| No state file (managed by AWS) | Maintains local or remote state |
| Deep AWS integration           | Community modules & plugins     |

---

### **7. What is a Nested Stack?**

A stack created as part of another stack. Useful for modular, reusable templates.

---

### **8. How does CloudFormation handle Rollbacks?**

If stack creation/update fails, CloudFormation automatically **rolls back** to the previous stable state.

---

### **9. What is Fn::GetAtt?**

A function used to fetch attributes of resources.
Example:

```yaml
!GetAtt MyEC2Instance.PublicIp
```

---

### **10. What is the difference between Ref and GetAtt?**

* **Ref** returns the default value of a resource (like ID).
* **GetAtt** returns specific attributes.

---

### **11. How do you pass data to EC2 using CloudFormation?**

Using **UserData** in the EC2 resource.

---

### **12. What are Output values used for?**

* Displays important information after stack creation (e.g., ALB URL)
* Can be exported for use in other stacks

---

### **13. How do you update a CloudFormation stack without downtime?**

* Use **Change Sets**
* Use **AutoScalingGroups with rolling updates**
* Use **UpdatePolicy**

---

### **14. What happens if a template is missing the Resources section?**

Stack creation fails because **Resources is mandatory**.

---

### **15. What is AWS::CloudFormation::Init?**

A metadata tool to configure EC2 instances (files, packages, services) during launch.

---

### **16. How do you store CloudFormation templates?**

* GitHub
* S3 Bucket
* AWS Service Catalog

---

### **17. What is Stack Policy?**

A JSON document that protects critical stack resources from unintentional updates.

---

### **18. How do you reuse common CloudFormation code?**

* Nested Stacks
* StackSets
* Modules

---

### **19. What is CloudFormation StackSet?**

Allows deployment of CloudFormation stacks **across multiple AWS accounts and regions**.

---

### **20. What is the use of Parameters?**

Makes templates dynamic and reusable.

---

