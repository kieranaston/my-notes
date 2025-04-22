# Security

## Shared responsibility model

AWS controls security of the cloud, while customers control security in the cloud.

Consider a homeowner and a homebuilder. The builder (AWS) is responsible for constructing your house and ensuring that it is solidly built. As the homeowner (the customer), it is your responsibility to secure everything in the house by ensuring that the doors are closed and locked.

## User permissions and access

AWS root user: Access and control any part of the account. You do not want to use the root user for everything of course.

You can control access in a granular way using AWS Identity and Access Management (AWS IAM). You can use this to create IAM users that by default do not have any permissions.

You have to explicitly give IAM users permissions to do anything in that account. Following the principle of least privilige, you only give users access to what they need.

An IAM policy is a JSON document describing what API calls a user can or cannot make.

One way to make it easier to manage your users and their permissions is to organize them into IAM groups. Groups are groupings of user policies.

## Roles

Roles have associated permissions that can allow or deny certain actions, and can be assumed for temporary amounts of time.

## AWS Organizations

AWS Organizations is a central location to manage multiple AWS accounts. Also has consolidated billing. Can also implement hierarchical groupings of accounts. Also have control over the AWS service and API actions access control.

### Service control policies (SCPs)

Enable you to place restrictions on the AWS services, resources, and individual API actions that users and roles in each account can access.

SCPs can be applied to organizational units and individual member accounts.

## Compliance

AWS complies with a long list of assurance programs.

### AWS Artifact

Gain access to compliance reports completed by third parties.

Suppose your company needs to sign an agreeement with AWS regarding your use of certain types of information throughout AWS services. You can do this through AWS Artifact Agreements.

Next, suppose a member of your company's development team is building an application and needs more information about their responsibility for complying with certain regulatory standards. You can advice them to access this information in AWS Artifact Reports.

## Denial-of-service attacks

Objective of DDoS attack is to shut down system by overwhelming it. Leverages other machines to unknowingly attacking your infrastructure. Key to a powerful attack if if the attacker creates the most work possible for the infrastructure while putting in the least amount of effort possible.

### UDP flood

Example is asking the weather service to send a bunch of information to a return address (the return address of the service you are trying to cripple) to overload it without it asking for that info.

Solution: Security groups that only allow in proper request traffic that we want.

### HTTP level attacks

Look like normal customers asking for normal things, but repeated over and over by bot machines.

### Slowloris Attack

Attacker pretends to have a terribly slow connection, meanwhile until their request finishes you can't move on to the next one.

Solution: Elastic load balancer. To overwhelm ELB you would have to overwhlem the entire AWS region.

### AWS Shield with AWS WAF

WAF uses a web application firewall to filter incoming traffic.

AWS Shield Standard automatically protects all AWS customers at no cost. It protects your AWS resources from the most common, frequently ocurring types of DDoS attacks.

AWS Shield Advanced is a paid service that provides detailed attack diagnostics and the ability to detect and mitigate sophisticated DDoS attacks.

## Additional security services

### AWS key management service (AWS KMS)

Enables you to perform envryption operations through the use of cryptographic keys. A cryptographic key is a random string of digits used for locking (encrypting) and unlocking (decrypting) data. Can use AWS KMS to create, manage, and use cryptographic keys.

Can choose specific levels of access control you need for your keys.

### AWS WAF

Web application firewall that lets you monitor network requests that come into your web applications.

Works together with CloudfFront and Application Load Balancer.

Uses a web access control list (ACL) to protect your AWS resources.

### Amazon inspector

Can perform automated security assessments, and returns a list of security findings.

### Amazon GUardDuty

Provides intelligent threat detection for your AWS infrastructure and resources. Identifies threats by continuously monitoring the network activity and account behavior within your AWS environment.

GuardDuty findings can be reviewed in the AWS management console.

**Source:** [AWS Cloud Practitioner Essentials](https://www.aws.training/Details/eLearning?id=60697), AWS Training & Certification.