# Configure an S3 Bucket + CloudTrail
-	AWS Simple Storage Service (S3) is a scalable and resilient storage service that will be used to store logs from monitoring apps like CloudTrail and Wazuh.
-	AWS CloudTrail records actions taken in my AWS account and creates audit trails.

### 1.	Create a bucket with an account regional namespace for strong ownership and governance controls.
### 2.	Enforce bucket owner and disable ACLs.
### 3.	Block public access.
### 4.	Enable bucket versioning.
a.	This allows me to restore from previous bucket versions, giving me an audit trail as well as recovery methods.
### 5.	Enable Server-Side Encryption with AWS S3-Managed Keys (SSE S3).
a.	Encrypts data at rest with AES-256.
### 6.	Create a Lifecycle Policy to Delete All Logs in the S3 Bucket after 60 Days
a.	Set to expire all objects after 30 days. Once items are expired, they are not fully deleted but rather marked for deletion and treated as non-current.

b.	Set to delete all marked objects 30 days after they become non-current.  <img width="975" height="254" alt="image" src="https://github.com/user-attachments/assets/b8e37471-5000-40bb-813f-9cf97539e1b7" />

### 7.	Create a CloudTrail Using the Newly Configured S3 Bucket as the Storage Location.
a.	Set a prefix “cloudtrail” for each log.
### 8.	Enable Log File SSE-KMS Encryption
### 9.	Create a New Customer Managed KMS Key and Alias
### 10.	Enable Log File Validation
a.	Log file validation allows CloudTrail to determine if logs were modified using integrity checks.
### 11.	Enable Management and Insight Event Logging
a.	Allowed CloudTrail to log read and write activity performed on AWS resources.

b.	Insight events allow logging for errors.
