# 🧠 **50 VPC Interview Questions (with Answers)**

### **1. What is a VPC?**

A logically isolated virtual network in AWS.

### **2. What is the difference between default and custom VPC?**

Default has pre-configured components; custom VPC requires manual setup.

### **3. Can a subnet span multiple AZs?**

No.

### **4. How many subnets can a VPC have?**

Up to 200 (can be increased).

### **5. Why are 5 IPs reserved in every subnet?**

For AWS internal networking (router, DNS, broadcast, etc.).

### **6. What is a public subnet?**

Subnet with IGW route.

### **7. What is a private subnet?**

Subnet with NAT or no internet access.

### **8. What is an isolated subnet?**

No internet capability.

### **9. Does IGW support IPv6 and IPv4?**

Yes.

### **10. Can we attach more than one IGW to VPC?**

No.

### **11. Can VPC CIDRs be modified?**

You can **add** new CIDRs but cannot shrink existing.

### **12. What happens if VPC CIDRs overlap?**

Communication fails; not allowed in peering.

### **13. What is VPC peering?**

Private connection between VPCs.

### **14. Does VPC peering support transitive routing?**

No.

### **15. What is transitive routing?**

VPC A → VPC B → VPC C routing. Only TGW supports this.

### **16. Difference between VPC Peering and Transit Gateway?**

TGW supports transitive routing and scale.

### **17. What is Route Table?**

Defines how traffic flows.

### **18. What's in every route table by default?**

The **local** route.

### **19. Can NAT Gateway be placed in private subnet?**

No.

### **20. Does NAT Gateway support inbound traffic?**

No, outbound only.

### **21. NAT Gateway vs NAT Instance?**

NAT Gateway is managed, scalable; NAT instance is EC2-based.

### **22. Can NACL deny traffic?**

Yes.

### **23. Can SG deny traffic?**

No.

### **24. NACL stateful or stateless?**

Stateless.

### **25. SG stateful or stateless?**

Stateful.

### **26. What is ephemeral port range?**

Ports 1024–65535.

### **27. What is Direct Connect?**

A dedicated network connection to AWS.

### **28. Difference between VPN and Direct Connect?**

VPN is encrypted, internet-based; Direct Connect is private, faster.

### **29. What is VPN tunnel?**

Encrypted communication path.

### **30. Components of Site-to-Site VPN?**

VGW + CGW.

### **31. What is VPC Endpoint?**

Private connection to AWS services.

### **32. Gateway vs Interface Endpoint?**

Gateway → S3, DynamoDB
Interface → All other services

### **33. What is ENI?**

Elastic Network Interface.

### **34. Can we attach multiple ENIs to an EC2?**

Yes.

### **35. What is secondary IP?**

Extra private IP on ENI.

### **36. Does ENI persist after instance stop?**

Yes.

### **37. Can an NACL block specific IPs?**

Yes.

### **38. Scenario: Application in private subnet needs internet.**

Use NAT Gateway.

### **39. Scenario: Two VPCs in different regions need connectivity.**

Use VPC Peering or TGW.

### **40. Scenario: Need secure access to S3 without internet.**

Use Gateway VPC Endpoint.

### **41. Scenario: Need central hub for 20 VPCs.**

Use Transit Gateway.

### **42. Scenario: On-prem network must connect to VPC.**

Use Site-to-Site VPN.

### **43. Scenario: Block malicious IP from an entire subnet.**

Use NACL deny rule.

### **44. Scenario: Restrict EC2 only to database traffic.**

Use Security Groups.

### **45. Scenario: Application needs dual-network interface.**

Attach multiple ENIs.

### **46. Can TGW connect VPCs and VPN?**

Yes.

### **47. What is TGW Route Table?**

Controls routing between attachments.

### **48. Can VPC Endpoint connect to internet?**

No, stays inside AWS network.

### **49. How many route tables can a VPC have?**

Unlimited (default + custom tables).

### **50. How to share VPC with multiple AWS accounts?**

Use AWS Resource Access Manager (RAM).

---
