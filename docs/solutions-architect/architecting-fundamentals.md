# Architecting fundamentals

## AWS services

* Secure and robust
* Lots of services
* Pay as you go

The main benefit is agility.

**Why customers move to AWS**:

* Agility
    * Accelerate time to market
    * Increase innovation
    * Scale seamlessly
* Complexity and risk
    * Optimize costs
    * Minimize security vulnerabilities
    * Reduce management complexity

### Categories of AWS services

**Serverless**:

* Amazon API Gateway
    * Create, publish, maintain, and secure RESTful and WebSocket APIs at any scale
* Amazon Simple Queue Service (Amazon SQS)
    * Message queuing service that decouples and buffers communication between distributed application components
* Amazon Simple Notification Service (Amazon SNS)
    * Messaging services enabling message delivery to multiple subscribers via push mechanisms like email, SMS, or Lambda
* Amazon Kinesis
    * Real-time data streaming and processing at scale, enabling ingestion and analysis of large volumes of streaming data such as logs, events, and video

**Networking and Content Delivery**:

* Amazon Virtual Private Cloud (Amazon VPC)
    *  Lets you create a private, isolated network within AWS where you can launch and manage your cloud resources
* VPC endpoints
    * Allow you to privately connect your VPC to AWS services without needing to go over the public internet
* VPC traffic security
    * Includes tools like security groups and network ACLs that help control who can send or receive data in your VPC
* VPC peering connection
    * A way to link two VPCs so they can communicate with each other using private IP addresses
* Hybrid networking
    * Connects your on-premises network to AWS so you can use both together smoothly
* AWS Transit Gateway
    * A central hub that makes it easier to connect multiple VPCs and on-premises networks all in one place

**Database**:

* Amazon Relational Database Service (Amazon RDS)
    * Makes it easy to set up, run, and scale traditional SQL databases in the cloud without managing the hardware
* AMazon DynamoDB, a NoSQL service
    * A fast, fully managed NoSQL database service designed for apps that need quick access to large amounts of unstructured data.

**Security, Identity, and Compliance**:

* Mechanisms to define identity and access management policies in AWS accounts
    * Use IAM policies and roles to control who can access which AWS resources and what actions they can take.
* AWS services which enable you to implement security and identity policies
    * Services like AWS IAM, AWS Organizations, and AWS Config help manage permissions, track changes, and enforce security rules.
* How to protect your AWS infrastructure from distributed denial of service (DDoS) attacks
    * AWS Shield and AWS WAF protect your applications by detecting and blocking harmful traffic before it reaches your services.

**Management and Governance**:

* AWS infrastructure management for applications
    *  Services like AWS Systems Manager and AWS Config help you monitor, manage, and maintain your cloud resources.
* AWS CloudFormation
    * Lets you describe your entire cloud setup in code so you can automate and consistently recreate your infrastructure.

**Storage**:

* Amazon Simple Storage Service (Amazon S3)
    *  A highly scalable object storage service used to store and retrieve any amount of data, like files, backups, and media.
* AWS Storage Gateway
    * Connects on-premises software with cloud storage to back up and archive data seamlessly.
* Amazon FSx
    *  Provides managed file systems in the cloud that support Windows, Lustre, and other workloads requiring shared storage.

**AWS Cost Management**:

* AWS Billing and Cost Management
    *  Helps you track your usage, manage budgets, and forecast or analyze your AWS spending.

**Containers**:

* Microservices architecture
    * A way to build applications as a collection of small, independent services that can be developed and deployed separately.
* Managing Microservices on AWS
    * Services like Amazon ECS, EKS, and AWS App Mesh help run, scale, and connect containerized microservices efficiently.

**Source:** [AWS Certified Solutions Architect - Associate (Subscription - Partner Subscription)](https://explore.skillbuilder.aws/learn/learning-plans/2159/aws-certified-solutions-architect-associate-subscription-partner-subscription), AWS Training & Certification.