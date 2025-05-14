# Amazon S3

A durable object storage solution.

Once you upload files to S3 they become objects in a bucket.

Good for data lakes for big data analytics.

Bucket names should be globally unique.

## What is an object?

An object is composed of a file and any metadata that describes that file.

## How to access objects in bucket?

Use bucket and object key. Object key is unique ID for object in bucket.

**Other use cases**:

* Backup and restore
* Data lakes for analytics
* Media storage and streaming
* Static websites
* Archiving and compliance

Think of S3 as a place to safely store your data in a replicated fashion.

Use cases of write-once-read-many are best served with S3.

Buckets are regional.

Data can be uploaded to buckets programmatically or through AWS Management Console.

## Key S3 features

### Accelerate innovation

Great for static files, no reliance on traditional file system.

### Increase agility

Flexible storage size, scaling.

### Reduce cost

Archive data and use different storage tiers to save.

### Strengthen security

Meet regulatory requirements.

## Cross-Region Replication (CRR)

Amazon S3 feature used to automatically copy new objects to a bucket in a different AWS Region.

## Event notification

Amazon S3 feature that can initiate an action to occur after an event takes place within a bucket.