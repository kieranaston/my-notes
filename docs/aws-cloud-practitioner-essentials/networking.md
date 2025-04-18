# Networking

## Amazon Virtual Private Cloud (VPCs)

A VPC lets you provision a logically isolated section of the AWS cloud where you can launch AWS resources in a virtual network that you define.

The private and public grouping of resources are known as subnets, and they are ranges of IP addresses in your VPCs.

Essentially your own private network in AWS. Allows you to define your private IP range for your AWS resources, and you place things like EC2 instances and ELBs (Elastic Load Balancers) inside of your VPC.

For some VPCs you might have internet-facing resources that the public should be able to reach, like a public website. In other scenarios you might have resources that you only want to be reachable if someone is logged into your private network, such as an HR application or backend database.

## internet gateway (IGW)

In order to allow traffic from the public internet to flow into and out of your VPC, you must attach what is called an internet gateway, or IGW, to your VPC. This is like a doorway that is open to the public.

## Virtual private gateway

If we don't want just anyone to be able to access these resources, we want a private gateway that only lets in people coming from an approved network.

This is called a virtual private gateway, and allows you to create a VPN connection between a private network (like your on-premises data center) and your VPC.

## Direct connect

The problem with using a VPN connection is they use bandwidth being shared by many people using the internet. To get around this you can use AWS direct connect, which allows you to establish a completely private, dedicated fiber connection from your data center to AWS. This can help with high regulatory and compliance needs, as well as any bandwidth issues.

One VPC might have multiple types of gateways attached for multiple types of resources all residing in the same VPC, just in different subnets.

## Subnets and network access control lists

### Subnets

Public subnets contain resources that need to be accessible by the public, such as an online store's website.

Private subnets contain resources that should be accessible only through your private network, such as a database that contains customers' personal information and order histories.

Internet gateways only cover the perimeter. We need to cover other layers of security as well.

### Network hardening

The only technical reason to use subnets in a VPC is to control access to gateways. Subnets can also control packet permissons. Every packet that tried to cross over the subnet boundary gets checked against the network access control list (network ACL). This is to see if the packet has permissions to leave or enter the subnet. Network ACL kinda acts like a border control officer.

By default, your AWS account's network access control list is stateless and allows all inbound and outbound traffic.

### Security groups

This does not solve the problem of different levels of security for different EC2 instances within the subnet though. You need instance-level security as well. For this we can use security groups. You can modify these groups to accept specific types of traffic. These are like a doorman at a building or hotel. You may been let into the country by the border control officer, but the doorman of the building might turn you away.

By default, security groups allow any traffic out and deny all incoming traffic. Key difference between network ACL and security group is a security group is stateful, meaning that it remembers what to let in or out. A network ACL checks every packet regardless.

## Global networking

### Amazon Route 53

Highly available and scalable DNS. Think of it as a translation service, but instead of translating languages, it translates website names into IP addresses.

Some of the route 53 routing policies:

* Latency based
* Geolocation DNS
  * Direct traffic based on where customer is located
* Geoproximity
* Weighted round robin

You can also use route 53 to buy and manage domain names.

### Amazon Cloudfront

Using edge locations with cached content to better serve content around the world using CDNs. A CDN is a network that delivers edge content to users based on their geographic location.

**Source:** [AWS Cloud Practitioner Essentials](https://www.aws.training/Details/eLearning?id=60697), AWS Training & Certification.