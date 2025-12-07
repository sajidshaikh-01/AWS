# 🧠 S3 Interview Questions (Deep + Scenario-Based)

## **1. What is Amazon S3?**

Object storage service with unlimited scalability and 11 9's durability.

## **2. Difference between S3 and EBS/EFS?**

| S3             | EBS           | EFS          |
| -------------- | ------------- | ------------ |
| Object storage | Block storage | File storage |
| Infinite       | Same AZ only  | Multi-AZ     |
| Not mountable  | Mountable     | Mountable    |

## **3. What is S3 Versioning? Why is it important?**

Protects against accidental delete/overwrite by maintaining object versions.

## **4. What is a delete marker?**

A marker that hides the latest version without deleting it.

## **5. Can versioning be disabled once enabled?**

No, can only be suspended.

## **6. What is S3 Transfer Acceleration?**

Uses CloudFront edge locations to accelerate uploads.

## **7. Why do static websites need CloudFront for HTTPS?**

S3 static hosting does not support SSL certificates.

## **8. What is SRR?**

Same-Region Replication – replicates objects within same region.

## **9. What is CRR?**

Cross-Region Replication – replicates objects across AWS regions.

## **10. Can CRR replicate existing objects?**

Yes, if explicitly enabled.

## **11. Does replication replicate delete markers?**

Optional; can be enabled.

## **12. Does CRR replicate storage class?**

Yes, unless overridden in rules.

## **13. Can encrypted objects be replicated?**

Yes, SSE-S3 works automatically. For SSE-KMS, permissions are needed.

## **14. Why is versioning required for replication?**

Replication must track object changes, hence versioning is mandatory.

## **15. What happens if destination bucket already has object with same key?**

Replication will not overwrite unless configured.

---
