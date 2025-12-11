# 🧪 . Scenario-Based Questions

## **Scenario 1: You need to trigger Lambda daily at 1 AM. What will you use?**

Answer: EventBridge Scheduled Rule
Pattern:

```cron
cron(0 1 * * ? *)
```

---

## **Scenario 2: You want to route EC2 STOP events to Slack.**

Answer:

1. Create Event Pattern for EC2 STOP
2. Target → Lambda that posts message to Slack

---

## **Scenario 3: You want microservices to communicate without API calls.**

Answer: Use **Custom Event Bus + EventBridge rules**.

---

## **Scenario 4: Lambda randomly fails when processing EventBridge events.**

Check:

* IAM target permissions
* Event size (max 256 KB)
* DLQ configuration

---

## **Scenario 5: You want to enrich an event before sending it to target.**

Use **EventBridge Pipes with Lambda enrichment**.

---




# 🎤 . Interview Questions & Answers

### **1. What is EventBridge?**

A serverless event bus for routing events between AWS services, applications, and SaaS systems.

---

### **2. What is the difference between EventBridge and SNS?**

| EventBridge                        | SNS                 |
| ---------------------------------- | ------------------- |
| Event router with filtering        | Pub/Sub messaging   |
| Supports event patterns            | Topic-based fan‑out |
| Integration with 200+ AWS services | Mostly messaging    |
| Can schedule events                | No scheduling       |

---

### **3. What is a Rule in EventBridge?**

Defines an event pattern + target to route matching events.

---

### **4. What are Event Buses?**

Channels where events are sent:

* Default
* Custom
* Partner

---

### **5. How does EventBridge handle failures?**

* Automatic retries (24 hrs)
* DLQ for failed deliveries

---

### **6. What is EventBridge Pipes?**

A direct point‑to‑point integration with filtering and enrichment.

---

### **7. What is Schema Registry?**

Stores event schemas and auto-generates code bindings.

---

### **8. How large can an EventBridge event be?**

Maximum **256 KB**.

---

### **9. How does EventBridge differ from Step Functions?**

* EventBridge = routing events
* Step Functions = orchestrating workflows

---

### **10. Can EventBridge send events cross‑account?**

Yes, using resource policies.

---


