# VPC fundamentals

Can imagine the VPC as a logical isolation for your workloads.

It is at the region level, and so can span different availability zones.

## Amazon Virtual Private Cloud

Your network environment in the cloud.

Can use VPC to launch AWS resources into virtual network you have defined.

Deployed into regions, can host resources from any AZ within region.

Using a VPC allows you to essentially create your own section of the cloud with your own rules, where your resources can live.

## Subnets

Range of IPs in your VPC.

AWS resources can be launched into a specific subnet.

A public subnet can be used for resources that are to be connected to the internet and a private subnet can be used for resources that won't be connected to the internet.

A subset resides in a single availability zone.

## Public subnets

Use:

* Internet gateways that allow your resources to communicate with the internet
* Route tables: rules VPC uses to route network traffic. In public subnet, includes route to internet gateway
* Public IP addresses that can be reached from the internet
* Private IP addresses that are only reachable on the network

## Internet gateways

Horizontally scaled. Redundant. Highly available.

Horizontal scaling is like adding more copies of something, while vertical scaling is like upgrading the existing copy.

Permits communication between instances within VPC and internet.

**Serves two purposes**:

1. Provides target in route table for internet-routable traffic.
2. Protects IP addresses on network by perfroming network address translation (NAT)

**Source:** [AWS Certified Solutions Architect - Associate (Subscription - Partner Subscription)](https://explore.skillbuilder.aws/learn/learning-plans/2159/aws-certified-solutions-architect-associate-subscription-partner-subscription), AWS Training & Certification.