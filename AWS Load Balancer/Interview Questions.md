# 🧠 Elastic Load Balancer Interview Questions & Answers

## **Q1: What is Elastic Load Balancer?**

A managed service that distributes traffic across multiple targets to ensure high availability.

---

## **Q2: What are the types of ELBs?**

* ALB
* NLB
* CLB
* GWLB

---

## **Q3: Difference between ALB and NLB?**

| Feature         | ALB               | NLB        |
| --------------- | ----------------- | ---------- |
| Layer           | 7                 | 4          |
| Routing         | Path/Host routing | No routing |
| Performance     | Moderate          | Extreme    |
| Sticky Sessions | Yes               | No         |
| Targets         | EC2, IP, Lambda   | EC2, IP    |

---

## **Q4: What is a Target Group?**

A group of resources (EC2/IP/Lambda) behind a load balancer.

---

## **Q5: What are health checks?**

Checks performed by the load balancer to decide if a target is healthy.

---

## **Q6: What is SSL termination?**

Decrypting SSL traffic at the load balancer instead of EC2.

---

## **Q7: What is sticky session?**

A feature that binds a user session to the same backend server.

---

## **Q8: What is cross-zone load balancing?**

Distributes traffic evenly across all availability zones.

---

## **Q9: Does ALB support WebSockets?**

Yes.

---

## **Q10: Can an ALB route traffic to Lambda?**

Yes. ALB supports Lambda as a target.

---

## **Q11: What is host-based routing?**

Routing based on domain/host header.
Example:

* api.example.com → TargetGroup1
* users.example.com → TargetGroup2

---

## **Q12: What is path-based routing?**

Routing based on URL path.
Example:

* /app → App targets
* /api → API targets

---

## **Q13: What is GWLB used for?**

For deploying firewalls, IDS, IPS, and traffic inspection.

---

## **Q14: Does NLB support static IP?**

Yes. NLB supports Elastic IPs.

---

## **Q15: What happens if all targets become unhealthy?**

Load balancer returns **503 Service Unavailable**.

---

