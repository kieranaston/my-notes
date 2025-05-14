# Securing objects

## Amazon S3 access control

By default all S3 resources are private. A resource owner can grant access permissions using access policies.

## Bucket policies

Resource-based policies for S3 buckets.

An example policy would be allowing any principal ot list the bucket and get any object from the bucket.

## Amazon S3 access points

Named network endpoints you can use to perform S3 object operations.

Access points are attached to buckets.

**Example**:

Finance employee assumes finance team IAM role, sends GetObject request to finance access point.

Access point policy allows finance role to get objects in the bucket with prefixes /finance and /tax.

S3 bucket policy allows finance access point to have access to your bucket.

## Server-side encryption key types

### Amazon S3-Managed Keys

Amazon S3 manages primary key that can create encryption keys for each object.

### AWS KMS keys

AWS Key Management Service is used to manage encryption keys.

### Customer-Provided Keys

You yourself as the customer manage the keys, while Amazon S3 manages encryption.

