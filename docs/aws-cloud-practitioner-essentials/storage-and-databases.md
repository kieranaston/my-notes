# Storage and databases

As EC2 instances run applications, those applications will often require block-level storage. In block level storage, when something is changed only that aspect is rewritten rather than the entire thing. This makes it an efficient storage type when working with databases, enterprise software or file systems.

## Instance stores and amazon elastic block store (Amazon EBS)

### Instance store volumes

When you launch an EC2 instance it might provide you with local storage called instance store volumes. These are physically attached to the host your EC2 instance is running on top of. You can write to it just like a normal hard drive. The problem here is that if you terminate the instance or host, all data in the instance store volumes will be deleted. This is because you often start up an instance on a different host.

So these are useful in situations where you can afford to lose the data being written to the drives.

### Amazon elastic block store (Amazon EBS)

If you do not want to be losing your database every time your instance is terminated, you can use Amazon EBS. This allows you to create virtual hard drives that are not attached to the host the EC2 instance is running on. The data persists through stops and starts of an instance.

EBS allows you to create incremental backups of your database called snapshots.

## Amazon simple storage service

Store and retrieve an unlimited amount of data. Store data as objects, in buckets.

in object storage, each object consists of data, metadata, and a key.

Maximum object size of 5 TB. Can version objects, and create multiple buckets.

Another way to use S3 is static website hosting (a bunch of static HTML files).

### Amazon S3 standard-infrequent access (S3 Standard-IA)

Used for data accessed less frequently, requires rapid access when needed. Good place to store backups, disaster recovery files, etc.

### Amazon S3 Glacier Flexible Retrieval

Good for retaining data for several years for auditing purposes. Can either move data to it or use vaults populated with archives. Can use a S3 Glacier Vault lock policy to meet compliance requirements (can use policies like write once/read many WORM).

### Amazon S3 Glacier Deep Archive

Good for archival data.

### Lifecycle policies

Policies that automatically move data between tiers. For example, keeping an object in S3 standard for 90 days then moving it to S3 standard IA for 30 days, and so on...

## Comparing Amazon EBS and Amazon S3

### Amazon EBS

* Sizes up to 16 TiB
* Survive termination of their EC2 instance
* Solid state by default
* HDD options

An EBS volume must be located in the same Availability Zone as the Amazon EC2 instance to which it is attached.

### Amazon Simple Storage Service (S3)

* Unlimited storage
* Individual objects up to 5 TBs
* Write once/read many
* 99.999999999% durability

**Difference between object storage and block storage**: Object storage treats any file as a complete, discrete object. Great for documents, images, and video files that get uploaded and consumed as entire objects. However, any time a change happens you must re-upload the entire file. Block storage breaks those files down into component parts, meaning that when you make an edit to one part, the edit only updates the blocks where those bits live.

If you are using only complete objects, S3 is victorious. If you are doing complex read/write change functions, then EBS is better.

## Amazon Elastic File System (Amazon EFS)

Managed file system. Common for businesses to have shared file systems across their applications. Might have multiple servers running analytics on data stored in a shared file system. With EFS you can leave the file system in place and let AWS handle all the scaling and replication.

EFS allows you to have multiple instances that can access the data in EFS at the same time. Scales up and down as needed.

Data in an Amazon EFS file system can be accessed concurrently from all the Availability Zones in the Region where the file system is located.

### What is the difference between EBS and EFS?

EBS volumes attach to EC2 instances and are an availability zone level resource. In order to attach EC2 to EBS you need to be in the same AZ. Volumes also do not automatically scale to give you more storage.

EFS can have multiple instances reading and writing simultaneously. It is a true Linux file system, and a regional resource. So any EC2 instance in the region can write to the EFS. Also automatically scales.

## Amazon relational database services

If you want to keep track of relationships between different data, you should use a relational database management system (RDBMS).

AWS supports multiple databases like MySQL, PostgreSQL, Oracle, and Microsoft SQL Server.

To migrate your databases to AWS you can perform a lift and shift to an EC2 instance.

You can also use a more managed service like Amazon Relational Database Service (Amazon RDS). Comes with automated patching, backups, redundancy, failover, disaster recovery, etc.

Amazon Aurora is another option that is even more managed. Comes in MySQL and PostgreSQL, and comes in at 1/10th the cost of commercial databases. Data is replicated across facilities, and you can upload up to 15 read replicas. There are also continuous backups to S3, so you always have a backup ready to restore.

Amazon Aurora is considered to be part of Amazon RDS.

## Amazon DynamoDB

At its most basic level it is a serverless database. You don't need to manage the underlying instances or infrastructure powering it. You can create tables populated with items that have attributes. The burden of operating an available database is much lower when using DynamoDB.

Does not use SQL. Rigid SQL databases can have performance and scaling issues when under stress. Might not be best for dataset that is not rigid and might be accessed at a very high rate.

DynamoDB is a non-relational database. You can add and remove attributes from items in a table anytime, and not every item in a table has to have the same attributes. You write queries based on a small subset of attributes designated as keys. Queries of this type generally focus on a collection of items from one table rather than across multiple tables. Allows it to be quick and scalable.

## Comparing Amazon RDS and Amazon DynamoDB

### Amazon RDS

* Automatic high availability; recovery provided
* Customer ownership of data
* Customer ownership of schema
* Customer control of network

### Amazon DynamoDB

* Key-value
* NoSQL
* Massive throughput capabilities
* PB size potential
* Granular API access

### Which one is right for you?

If you need complex relational joins between tables, you need RDS. For pretty much anything else, you could use DynamoDB. If you basically just need lookup tables (single table stuff), DynamoDB would be great.


## Amazon Redshift

Once data becomes too complex to handle with traditional relational databases, you've entered the world of data warehouses. Good for historical analytics. As long as your data question involves looking backward, then a data warehouse could be right for that situation.

Amazon Redshift is data warehousing as a service, and is massively scalable. Can achieve much better performance compared to other database technologies for these kinds of queries. When you need big data business intelligence solutions, Redshift is a good choice.

## AWS Data Migration Service

Does AWS have a magical way to help you migrate your existing database?

Essentially migrate data between a source database and target database, with the source database remaining fully operational during the migration. The source and target databases don't even have to be the same type.

### Homogeneous databases

Migration between two databases of same type. The source database could be on premises running on EC2 instances, or can be an Amazon RDS database. The target database can be Amazon EC2, or Amazon RDS.

### Heterogeneous migration

When the source and target are of different types. 2-step process, uses conversion tool to match the schema and database code, then you migrate it.

**Other use cases**:

* Development and test database migrations
    * When you want your developers to test against production data but without affecting production users, so you create a copy
* Database consolidation
    * When you have several databases and want to combine them into one
* Continuous replication
    * When you use DMS to perform continuous database replication (disaster recovery, or geographic separation)

## Additional database services

What if you need a full content management system?

### Amazon DocumentDB (MongoDB compatability)

Content management, catalogs, user profiles, etc.

What if you had a social network and wanted to see who is connected to who etc.?

### Amazon Neptune

Graph database engineered for social networking. Also great for fraud detection needs. Or tracking a supply chain, or banking records requiring 100% immutability.

### Amazon Managed Blockchain

Blockchain solution.

### Amazon Quantum Ledger Database

immutable records where any entry can never be removed from the audits.

## Database accelerators

Caching layers that can hlp improve the read times of common requests.

### Amazon ElastiCache

Caching layers without heavy lifting.

### Amazon DynamoDB Accelerator

An in-memory cache for DynamoDB.

**Source:** [AWS Cloud Practitioner Essentials](https://www.aws.training/Details/eLearning?id=60697), AWS Training & Certification.