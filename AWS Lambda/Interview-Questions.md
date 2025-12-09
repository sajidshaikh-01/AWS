# Interview Questions & Answers

### **1. What is AWS Lambda?**

Serverless compute service that executes code in response to events.

### **2. What causes Lambda Cold Starts?**

* New execution environment
* Scaling up
* No provisioned concurrency

### **3. Difference between Synchronous vs Asynchronous invocations?**

* Sync: Caller waits for response
* Async: Caller does not wait; Lambda retries on failure

### **4. What is an Event Object?**

Payload input passed to Lambda containing data from event source.

### **5. What is a DLQ?**

Queue that stores failed async Lambda events.

### **6. How do you connect Lambda to RDS?**

* Put Lambda in same VPC
* Allow SG access
* Use RDS Proxy

### **7. What is Provisioned Concurrency?**

Pre-warms environments to eliminate cold starts.

### **8. What is Lambda Layer?**

A way to share libraries across functions.

### **9. What is Lambda Alias?**

Pointer to Lambda version; supports canary deployments.

### **10. What are Lambda Destinations?**

Routing success or failure responses of async Lambda to SQS/SNS/EventBridge/Lambda.
