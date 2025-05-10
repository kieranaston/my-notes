# Storage for EC2 instances

## Amazon EBS volumes

One of the key features of EBS is that volumes can be attached and removed from different instances.

Can create EBS snapshots.

After you attach one to an instance you use it as you would a physical hard drive.

Multiple EBS volumes can be attached to a single instance.

### SSD volumes

Good for frequent read/write operations with small I/O size.

### HDD volumes

Good for large streaming workloads where main concern is throughput.

## Instance store volumes

Locally attached to host. Live for as long as the virtualization does, non-persistent.

**Source:** [AWS Certified Solutions Architect - Associate (Subscription - Partner Subscription)](https://explore.skillbuilder.aws/learn/learning-plans/2159/aws-certified-solutions-architect-associate-subscription-partner-subscription), AWS Training & Certification.