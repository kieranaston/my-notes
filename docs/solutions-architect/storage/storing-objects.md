# Storing objects

## Amazon S3 storage classes

In order from higher cost, frequent access, to lower cost, infrequent access:

**S3 Standard**: For general purpose storage of frequently accessed data.

**S3 Standard Infrequent Access**: For long-lived, but less frequently accessed data.

**S3 One Zone-Infrequent Access**: For long-lived, less frequently accessed data that can be stored in a single Availability Zone.

**S3 Glacier Instant Retrieval**: Archive data that is rarely accessed but requires a restore in milliseconds.

**S3 Glacier Flexible Retrieval**: Access all the archives you need, when you need them, for one low storage price.

**S3 Glacier Deep Archive**: Long-term cold storage archive, digital preservation. Objects can be restored in 12 hours or less.

## Amazon S3 Intelligent-Tiering

Data moves between access tiers as usage patterns change so that you can save on costs.

Works well for data with unknown, changing, or unpredictable access patterns, independetn of object size or retention period.

## Amazon S3 Glacier storage class benefits

* Cost-effective - lowest cost because you are committing to less frequent access
* Flexible data retrieval - three different storage classes with variable access options
* Secure and compliant - encryption at rest, AWS CloudTrail integration and retrieval policies
* Scalable and durable - meets scalability requirements, high durability

## Lifecycle policies

Used to transition objects to another storage class based on age of object.

Can have data cycled at regular intervals between different Amazon S3 storage types.

## Replicating S3 objects

**Replicate objects while retaining metadata**: Ensure replica is identical to source object if necessary.

**Replicate objects into different storage classes**: Replicate objects into S3 Glacier Flexible Retrieval, S3 Glacier Deep Archive, or another storage class in destination buckets.

**Maintain object copies under different ownership**: Tell S3 to change replica ownership to the AWS account that owns the destination bucket.

**Keep objects stored over multiple AWS Regions**: Meet compliance by replicating data to another region. 