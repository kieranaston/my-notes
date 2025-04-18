# Compute in the cloud

## Amazon EC2

EC2 refers to the servers that are used to run the virtual servers.

AWS is already running a massive amount of compute capacity, and you can use however much of that capacity you want, whenever you want.

You just request the EC2 instances you want, and they will boot up and be ready to use in just a few minutes.

Once you're done you can easily terminate those instances.

You only pay for what you use. You only pay for running instances, not stopped or terminated ones.

EC2 runs on top of physical host machines managed by AWS using virtualization. You are sharing the host with other instances (virtual machines). A hypervisor on the host machine is responsible for sharing the underlying physical resources between the virtual machines.

This is called multi-tenancy. Hypervisor coordinates this. Hypervisor isolates VMs from each other as they share resources from the host.

One EC2 instance is not aware of other EC2 instances even though they are on the same host.

When you provision an EC2 instance you can choose the operating system (Windows or Linux).

Beyond the OS you also configure what software you want running on the instance.

You might start with a small instance, and then if it starts to max out that server you can give the instance more memory and more CPU (vertically scaling an instance). You can do this whenever you need this.

You also control networking (types of requests, publicly or privately accessible).

## AWS instance types

Gives you flexibility of choosing appropriate distribution of resources for your applications.

### General purpose

Balanced. Used for variety of diverse workloads.

### Compute optimized

Compute intensive tasks. Gaming servers, high performance computing (HPC), etc.

### Memory optimized

Good for memory intensive tasks, like high-performance databases.

### Accelerated computing

Floating-point number calculations, graphics processing, data pattern matching.

### Storage optimized

Workloads that require high performance for locally stored data.

## EC2 pricing

### On-demand

Only pay for running duration. No long-term commitments. Good for getting up and running and testing workloads.

### Savings plans

Low pricing, commitment to specific usage terms of a year or a few.

Reduce you instance costs when you make an hourly spend commitment to an instance family and region for a 1-year or 3-year term.

### Reserved instances

Workloads with predictable usage. Can pay full upfront, partial upfront, and no upfront. Standard reserve instances require you to specify instance family and size, platform description, tenancy, and region.

Available over 1-year or 3-year term.

### Spot instances

Get spare computing capacity, but can be reclaimed any time it is needed with a 2 minute warning. Good for batch owrkloads.

### Dedicated hosts

Usually for meeting certain compliance requirements, and nobody else will be using that host.

## Scaling Amazon EC2

Scalability and elasticity refers to how capacity can grow and shrink based on business needs.

Do not want to end up with data centers under 10% average utilization for fear of missing out on peak demand.

Amazon EC2 auto scaling enables you to automatically add or remove Amazon EC2 instances in response to changing application demand.

**Dynamic scaling** responds to changing demand.

**Predictive scaling** automatically schedules the right number of Amazon EC2 instances based on predicted demand.

### Auto scaling

When creating an auto scaling group you can set the minimum number of Amazon EC2 instances that start up as soon as you create the auto scaling group (minimum capacity). You can also set the desired capacity even though your application needs a minimum of a single Amazon EC2 instance to run (desired capacity defaults to minimum capacity if not specified). Next you can set the maximum capacity so that you can scale out with demand but not past a maximum.

## Elastic load balancing

Say we have an uneven distribution of traffic across our EC2 instances. We need a host to direct customers to different lines to place their order, managing the distribution of traffic.

We apply this to AWS environments as elastic load balancing.

Load balancer is application that takes in requests and routes them to different instances to be processed. Many off the shelf solutions that work great with AWS.

AWS can provide this service in the form of Elastic Load Balancing. This is an AWS managed service that addresses issue of load balancing.

Because it runs at the region level rather than on specific EC2 instances, the service is automatically highly available with no additional effort on your part.

## Messaging and queueing

### Tightly-coupled architecture

If a single component has a problem it causes problems for other components or the whole system.

Applications made up of tightly coupled components are monolithic.

### Loosely coupled architecture

Single failure won't cause cascading failures.

You have a queue in the middle where messages go to eventually be processed. If a given application can't process the message, it stays in the queue until it is processed by another application.

### Amazon SQS (Amazon Simple Queue Service)

Allows you to send, store, and receive messages between software components at any volume, without losing messages or requiring other services to be available.

**Payload** is the data inside the message, and it is protected until delivery.

SQS queues are where messages are placed until they are processed.

### Amazon SNS (Amazon Simple Notification Service)

Amazon SNS can send out messages but it can also send out notifications to end users. Uses a publish subscribe model.

Can make an Amazon SNS topic: a channel for messages to be delivered. Can then configure subscribers for that topic, and publish messages for subscribers.

Subscribers can be web servers, email addresses, AWS Lambda functions, or several other options.

## Additional compute services

Though EC2 is good in a lot of cases, depending on your use case you might want an alternative.

When using EC2 you are responsible for setting up and managing your instances over time.

AWS offers multiple serverless compute options, meaning that you don't see or access the underlying infrastructure tha`t is hosting your application. Instead, all management of the underlying environment is taken care of. All you need to do is focus on your application.

### Serverless computing

When computing with virtual servers you have to think about the servers and code, while when serverless computing you only have to think about the code.

### AWS Lambda

AWS Lambda is a serverless compute option. More suited for quick processes, not something like deep learning.

Allows you to run code without needing to provision or manage servers. You can run code for virtually any type of application or backend service, all with zero administration.

Setup:

1. Upload code to Lambda
2. Set code to trigger from an event source
3. Code only runs when triggered
4. Pay only for the compute time you use

### Amazon Elastic Container Service (Amazon ECS)

Containers provide you with a standard way to package your application's code and dependencies into a single object. Can also use containers for processes and workflows in which there are essential requirements for security, reliability, and scalability.

Using containers could delp to ensure that the application's environment remains consistent regardless of deployment.

ECS supports Docker containers. With Amazon ECS you can use API calls to launch and stop Docker-enabled applications.

### Amazon Elastic Kubernetes Service (Amazon EKS)

Amazon EKS is a fully managed service that you can use to run Kubernetes on AWS. Kubernetes is open-source software that enables you to deploy and manage containerized applications at scale.

### AWS Fargate

Serverless compute engine for containers. Works with both Amazon ECS and Amazon EKS. When using Fargate, you do not need to provision or manage servers. Fargate manages the server infrastructure for you.


**Source:** [AWS Cloud Practitioner Essentials](https://www.aws.training/Details/eLearning?id=60697), AWS Training & Certification.