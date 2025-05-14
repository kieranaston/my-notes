# VPC traffic security

Network ACLs act as stateless firewall on the entire subnet.

Security groups are virtual firewalls acting on the instance level.

## Inbound and outbound IPv4 traffic

Every default VPC comes with a modifiable default network ACL. By default it allows all inbound and outbound IPv4 traffic.

Custom ACLs by default deny all inbound and outbound traffic.

## Network ACL rules

**Components of a network ACL rule:**

* Rule number
* Type (type of traffic)
* Protocol
* Port range (listening port for the traffic)
* Source (for inbound traffic)
* Destination (for outbound traffic)
* Allow or deny

## Security groups

These allow traffic based on IP protocol, port, or IP address and use stateful rules.

By default they include an outbound rule allowing all outbound traffic. If no outbound rules, no outbound traffic from that instance.

Security groups are stateful.

### Security group chaining

With a chain of security groups you can set up inbound and outbound rules in a way so that the traffic can only flow from top tier to bottom and back again.

## Security groups vs. Network ACLs

* Security groups are a firewall for EC2 instances, and network ACLs are a firewall for subnets
* Security groups control traffic at instance level, and ACLs control traffic at subnet level
* Security groups only support allow rules, while network ACLs support both allow and deny rules
* Security groups are stateful while network ACLs stateless
* Security groups need to be assigned to instances while network ACLs automatically applied when instances added to subnet

## How to make a subnet public?

Route outbound traffic through the internet gateway.

**Source:** [AWS Certified Solutions Architect - Associate (Subscription - Partner Subscription)](https://explore.skillbuilder.aws/learn/learning-plans/2159/aws-certified-solutions-architect-associate-subscription-partner-subscription), AWS Training & Certification.