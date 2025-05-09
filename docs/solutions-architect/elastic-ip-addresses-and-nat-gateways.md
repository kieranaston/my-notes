# Elastic IP addresses and NAT gateways

## Elastic IP address

Elastic IP address is static, public IPv4 address for dynamic cloud computing.

It can be associated with any instance or network interface for any VPC in your account.

Can mask failure of an instance by quickly remapping address to another instance in VPC.

Purpose is to permit association with instance or network interface.

Can be thought of as a business phone number - you keep same one even if you move offices or switch phones.

## Elastic network interface

Virtual network interface that:

* Can be moved amongst different instances in same AZ
* Maintains same IP address, elastic IP address, MAC address

## NAT gateways

Using NAT, private IP networks (like for databases and backend services) using unregistered IP addresses are able to connect to the internet.

One-way outbound connection between pricate subnet instances and internet or other AWS services.

## Associate elastic IP addresses with resources

Elastic IP address can be associated with any instance or network interface in any VPC.

## Connecting private subnets to the internet

NAT gateway can be used as a one-way connection between private subnet instances and the internet or other aws services.

**How to connect component in private subnet to internet:**

1. Route table for private subnet sends all IPv4 internet traffic to NAT gateway
2. NAT gateway uses Elastic IP as source IP for traffic from private subnet
3. Route table for public subnet sends all internet traffic to internet gateway. Not supported for IPv6

## Deploy VPC across multiple availability zones

This creates architecture achieving high availability, distributing traffic while secure.

If you have an outage in one AZ you can fail over to other.

**Source:** [AWS Certified Solutions Architect - Associate (Subscription - Partner Subscription)](https://explore.skillbuilder.aws/learn/learning-plans/2159/aws-certified-solutions-architect-associate-subscription-partner-subscription), AWS Training & Certification.