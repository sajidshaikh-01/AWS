# 🧠 CloudFront Interview Questions (With Answers)

### 1. What is CloudFront?

A global CDN service that caches content at edge locations to reduce latency.

### 2. What are the types of origins in CloudFront?

* S3
* EC2
* ALB
* API Gateway
* Any HTTP server

### 3. What is CloudFront Invalidation?

Removes objects from cache to ensure latest version is served.

### 4. How do you restrict S3 access only to CloudFront?

Use **Origin Access Control (OAC)**.

### 5. What is the purpose of Geo Restriction?

Block or allow certain countries from accessing your content.

### 6. How does CloudFront improve performance?

Caches content at global edge locations.

### 7. What is Path-Based Routing?

Route requests to different origins based on URL patterns.

### 8. Can CloudFront serve private content?

Yes, using Signed URLs or Signed Cookies.

### 9. What happens if you update content in S3?

CloudFront may still serve cached content → requires invalidation.

### 10. How to protect EC2 behind CloudFront?

Allow connections ONLY from CloudFront IP ranges.
