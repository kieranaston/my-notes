# Global infrastructure and reliability

High availability and fault tolerance is important. AWS operates in many regions to support this.

## AWS global infrastructure

Events could happen that could cause lost connection to a certain data center. Most businesses end up just using backups and hoping for no disasters.

If disaster strikes, AWS data centers will be fine. They build large data centers in central, business heavy locations.

Each of these regions contain multiple data centers that have all the compute, storage, and services you need. Each region is connected to each other region through a high speed fiber network. You get to choose which region you want to run out of. None of your data will come into or out of that region. It is isolated.

You might have certain government compliance requirements. E.g., any data in the Frankfurt region never leaves the Frankfurt region, unless you explicitly (with proper credentials) request an export.

Proximity and compliance both matters. Latency is always a factor.

Sometimes the obvious region choice may not have all of the AWS services/features available. Sometimes brand new services require new hardware and are difficult to implement everywhere.

If budget is primary concern, you might want to operate in a different country with different pricing.

## Availability zones

You don't want ot run your business out of a single building, or a single location.

AWS has lots of data centers all around the world. Each region is made up of multiple data centers. We refer to these groups of data centers as availability zones (one or more data centers with redundant power, networking, connectivity, etc.).

Each region consists of multiple isolated availability zones.

As best practice it is recommended that you always run across at least two availability zones in a region, in case one gets taken out.

## Edge locations

What if there is not an obvious answer to the problem of proximity for your business. You can instead cache a copy of your data locally, close to cutomers around the world. This uses concept of Content Delivery Networks (CDNs).

### Amazon Cloudfront

Service that helps deliver data, video, applications and APIs to customers around the world with low latency and high transfer speeds. Uses edge locations all around the world to accelerate communications with users no matter where they are.

Can push content from a region to a colletion of edge locations around the world to accelerate communication and content delivery.

AWS edge locations also run DNS called Amazon Route 53, directing customers to the correct web locations with reliably low latency.

AWS Outposts involve basically installing a fully operational mini region right inside your own data center. If you have specific problems that can only be solved by staying within your own building, it would be right for you.

## How to provision AWS resources

In AWS everything is an API call.

You can use tools like:

* AWS Management Console
* AWS Command Line Interface (CLI)
* AWS Software Development Kits (SDKs)
* Various other tools

To create requests to send to the AWS APIs to creat and manage AWS resources.

### AWS Management console

Browser based, manage visually. Useful for building test environments, AWS bills, view monitoring, and working with non-technical resources.

### AWS CLI

Allows you to make API calls using the terminal on your machine. Makes actions scriptable and repeatable.

### AWS SDKs

Allow you to interact through various programming languages.

### AWS Elastic Beanstalk

Allows you to provision Amazon EC2 based environments. You can just provide your application code and desired configurations to AWS Elastic Beanstalk service, which then takes that info and builds out your environment for you. Can also easily save environment configurations so that they can be deployed again.

Gives convenience of not having to provision and manage these things separately, while still giving the visibility and control of underlying resources.

### AWS Cloudformation

Infrastructure as code tool. Allows you to define wide variety of AWS resources with JSON or YAML text-based documents called cloud-formation templates. Allows you to define what you want to build without specifying exatly how you want to build it.

**Source:** [AWS Cloud Practitioner Essentials](https://www.aws.training/Details/eLearning?id=60697), AWS Training & Certification.