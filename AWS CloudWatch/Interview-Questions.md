# 🗂 11. CloudWatch Interview Questions & Answers

### **1. What is CloudWatch?**

A monitoring and observability service for logs, metrics, alarms, and dashboards.

### **2. Explain CloudWatch Namespace.**

A namespace groups related metrics (AWS/EC2, AWS/Lambda, Custom/MyApp).

### **3. Difference Between Logs and Metrics.**

* **Logs** → raw text data
* **Metrics** → numeric values representing performance

### **4. What is CloudWatch Agent?**

Agent that collects:

* OS metrics
* Application logs
* Custom metrics

### **5. How do you create custom metrics?**

Using AWS CLI, SDKs, or CloudWatch Agent.

### **6. What is the difference between Alarm States?**

* OK
* ALARM
* INSUFFICIENT DATA

### **7. What is a Log Retention Policy?**

Time period after which CloudWatch deletes logs.

### **8. Can CloudWatch trigger Auto Scaling?**

Yes, via alarms.

### **9. Why Billing Alarm Works Only in `us-east-1`?**

Account-level metrics are only published in the N. Virginia region.

### **10. How to monitor EC2 memory usage?**

Install CloudWatch Agent because memory metrics are not provided by default.
