# Migration and innovation

## AWS cloud adoption framework (CAF)

Guidance for moving over to cloud.

Divides guidance into six perspectives:

* Business perspective
  * Create a business case for cloud adoption
* People perspective
  * Evaluate organizational structures and roles, new skill and process requirements, identify gaps
* Governance perspective
  * Understand how to update the staff skills and processes necessary to ensure business governance in the cloud
* Platform perspective
  * Implementing new solutions on the cloud, migrating on-premises workloads to the cloud
* Security perspective
  * Selection and implementation of security controls that meet the organization's needs
* Operations perspective
  * Enable, run, use, operate, recover IT workloads to level agreed upon with business stakeholders

# Migration

6 strategies for migration:

* Rehosting
  * Moving applications without changes
* Replatforming
  * Making a few cloud optimizations without changing core application architecture
* Refactoring/re-architecting
  * Reimagining how an application is architected and developed by using cloud-native features
  * Driven by need to add features, scale, performance
* Repurchasing
  * Moving from traditional license to software-as-a-service model
  * Replacing an existing application with a cloud-based version
* Retaining
  * Keeping applications that are critical for the business in the source environment
* Retiring
  * Removing applications that are no longer needed

## AWS snow family

Collection of physical devices that help to physically transport up to exabytes of data into and out of AWS.

### AWS Snowcone

Small, rugged, and secure edge computing and data transfer device. 2 CPUs, 4 GB of memory, 14 TB of usable storage.

### AWS Snowball

Snowball edge storage optimized devices well suited for large-scale data migrations and recurring transfer worklows, local computing higher capacity needs.

Snowball edge compute optimized provides powerful computing resources for use cases like ML.

### AWS Snowmobile

Exabyte-scale data transfer service used to move large amounts of data to AWS.

Up to 100 petabytes of data per Snowmobile, 45-foot long ruggedized shipping container, pulled by a semi trailer truck.

## Innovation with AWS

Focus on desired outcomes: current state, desired state, and problems you are trying to solve.

### Serverless applications

Don't require you to provision, maintain, or administer servers. AWS Lambda is example.

### Artificial intelligence

For example:

* Convert speech to text with Amazon Transcribe
* Discover patterns in text with Amazon Comprehend
* Identify potentially fraudulent online activities with Amazon Fraud Detector
* Build voice and text chatbots with Amazon Lex

### Machine learning

Amazon SageMaker to remove difficult work from process and empower you to build, train, and deploy ML models quickly.

## Amazon Q Developer

ML code generator. Analyzes, generates comments. Automatically generates suggestions. Can be used as IDE extension.

**Source:** [AWS Cloud Practitioner Essentials](https://www.aws.training/Details/eLearning?id=60697), AWS Training & Certification.