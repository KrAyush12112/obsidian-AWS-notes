## **2. Object Storage**

Stores data as objects (good for unstructured data, backups, media).

- **S3 (Simple Storage Service)** → Scalable, durable storage for any data.
    
    - Storage Classes:
        
        - **S3 Standard** → Frequent access
            
        - **S3 Intelligent-Tiering** → Automatic cost optimization
            
        - **S3 Standard-IA** → Infrequent Access
            
        - **S3 One Zone-IA** → Single AZ, cheaper
            
        - **S3 Glacier Instant Retrieval** → Archival, seconds retrieval
            
        - **S3 Glacier Flexible Retrieval** → Hours retrieval
            
        - **S3 Glacier Deep Archive** → Cheapest, long-term archive
            
- **S3 on Outposts** → S3 but on your own hardware via AWS Outposts.