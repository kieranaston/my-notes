# AWS infrastructure

## AWS data centers & availability zones

Undisclosed facilities.

Use proprietary AWS resources.

Availability zones are the most granular form that we refer to when talking about data centers. Availability zones are clusters of data centers, and are interconnected. They help to protect against localized failures.

When you launch an instance, you can select an Availability Zone or let AWS choose one for you.

## AWS regions

Isolated from each other, can have multiple per country. Contain multiple availability zones.

Every time you see something like: us-east-1

This means we are talking about the first region of the east of the US.

If you see us-east-1b, we are talking about an availability zone.

Sometimes a service might be deployed in an availability zone, and sometimes it might be deployed in a region.

## Factors impacting region selection

* Governance
    * You should consider legal requirements
* Latency
  * Close proximity to customers means better performance
* Service availability
  * Not all AWS services are available in all Regions
* Cost
  * Different Regions have different costs

## AWS Local Zones

Specific locations that have small, specific amount of services available for workloads that require low latency like live streaming, etc.

Essentially for highly demanding applications that require single-digit millisecond latency to end users.

## Edge locations

Locations around the world that has limited number of services, like Route 53 or CloudFront (which caches data at these locations).

So if you have workloads where you are cachine content and want to increase probability that this content will be cached close to users, this might be for you.

Use case of edge locations is to bring the content closer to the customer for better performance.

## AWS Local Zone and edge location features

**AWS Local Zones**:

* Can run compute, storage, and databases
* Low latency
* Local data processing
* Consistent AWS experience

**Edge locations**:

* Caching of data
* Fast delivery of content
* Better user experience

**Source:** [AWS Certified Solutions Architect - Associate (Subscription - Partner Subscription)](https://explore.skillbuilder.aws/learn/learning-plans/2159/aws-certified-solutions-architect-associate-subscription-partner-subscription), AWS Training & Certification.