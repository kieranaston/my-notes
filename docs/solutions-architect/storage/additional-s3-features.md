# Additional S3 features

## Amazon S3 event notifications

Receive notifications when certain object events happen in bucket.

No longer have to implement server-based polling to check for object changes.

Notifications can be sent by S3 to the following destinations:

* Amazon SNS topics
* Amazon SQS queues
* AWS Lambda function

## Amazon S3 multipart upload

Consistently upload large objects in manageable parts.

1. Initiate upload
2. Upload parts
3. Complete upload

Once the multipart upload is finished, S3 will re-create the full object from the individual pieces.

## Amazon S3 Transfer Acceleration

Uses edge locations to facilitate fast data transfer into an S3 bucket.

Data is routed to Amazon S3 over an optimized network path.

Useful when:

* Have customers all over the world who upload to centralized bucket
* Transfer gigabytes or terabytes of data across continents on regular basis
* Unerutilize available bandwidth when uploading to Amazon S3 over the internet

## Amazon S3 cost factors

**Storage**: Cost can depend on size, length of storage, and storage class.

**Requests and retrievals**: You pay for requests made against your S3 buckets and objects. Costs based on request type, and charged on the quantity of requests.

**Data transfer**: Usually no transfer fee for data-in from the internet, and depending on requestor location and type of data transfer, there are different charges for data-out.

**Management and analytics**: You pay for the storage management and analytics features for your buckets.

**S3 replication and versioning**: You pay for each PUT request in addition to the storage tier charge for replication and versioning.