# EC2 instances

## Instance type names

**Example**:

c6g.xlarge

c is the instance family.

6 is the instance generation.

g is additional properties.

The part after the dot is the instance size.

## Benefit of new generation instances

Can see cost and performance benefits from the newer generation instances.

## Amazon EC2

Like your traditional on-premises server, but available in the cloud.

### EC2 instance launch considerations

**Name and tags**:

* Can assign metadata in form of tags
* Use these to locate and filter instances

**Application and OS image**:

* Which application and OS?

**Instance type and size**:

* What are your technical requirements?

**Key pair**:

* How will your instance be connected with other components and how will these connections be authenticated?

**Network and security**:

* What VPC, subnet, security groups?

**Configure storage**:

* What type of storage is best for your use case?

**Placement and tenancy**:

* Where should you run your EC2 instances

**Scripts and metadata**:

* What can you do to automate your launch?

## Amazon Machine Image (AMI)

Like a template for launching an instance.

Can be custom made or provided by AWS.

## EC2 instance families

You should pick the best instance family for your workload.

**General purpose**:

* Pretty balanced, diverse workloads
* Web applications

**Compute optimized**:

* Good for compute-bound applications
* Stuff like scientific modeling and machine learning

**Memory optimized**:

* Fast delivery of large datasets in memory
* Good for stuff like database servers, web caches, and data analytics

**Accelerated computing**:

* GPU bound tasks
* Machine learning, autonomous vehicles, etc.

**Storage optimized**:

* High sequential read/write
* Large datasets, NoSQL databases, etc.

## AWS Compute Optimizer

Uses machine learning to analyze configuration of your resources and usage from CloudWatch.

Will give you recommendations you can use to reconfigure and reduce costs, increase performance.

## Amazon EC2 key pairs

Consists of private key and public key.

Set of security credentials you use to prove identity when connecting to instance.

Amazon EC2 stores public key, you store private key.

You use private key to securely access your instances.

## Tenancy

**Shared tenancy**: Multiple AWS accounts might share the same physical hardware.

**Dedicated instance**: Physically isolated at the host hardware level from instances that are not dedicated and from other AWS accounts.

**Dedicated host**: Instances run on physical server fully dedicated to you.

## Placement groups, use cases

* Cluster placement groups recommended for low latency, high throughput applications
* Spread placement groups good for applications with small number of critical instances that need to be separate from each other
* Partition placement groups are good for large distributed and replicated workloads, and for avoiding same-time hardware failures

## User data

Can pass info like bash scripts to instance on startup.

**Source:** [AWS Certified Solutions Architect - Associate (Subscription - Partner Subscription)](https://explore.skillbuilder.aws/learn/learning-plans/2159/aws-certified-solutions-architect-associate-subscription-partner-subscription), AWS Training & Certification.