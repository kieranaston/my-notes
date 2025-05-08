# Managing multiple accounts

## Reasons to use multiple accounts

* Many teams
* Security and compliance
* Billing and cost insights
* Isolation
* Business process

## AWS Organizations

Put a bunch of accounts in one place where you can manage them all from.

Can further group those accounts into organizational units (OUs) and apply different access policies to each.

**Key characteristics**:

* Consolidated billing
* Centralized management
* Hierarchical grouping
* Integration w/ IAM
* Integration w/ AWS services

## With vs. without AWS organizations

Without organizations, applying a standardized policy would mean redundantly applying the same policy across many accounts. With organizations you can use service control policies to specify max permissions for accounts in organization.

## IAM policies with SCPs

Apply SCP to organization to define guardrail. Attach IAM policies to users or resources.

### Example

Could have an Organizations SCP allowing ec2 and s3.

Could have IAM identity-based permissions allowing ec2 and iam.

These interact, and what ends up being allowed is ec2 because it is explicitly allowed by both.

**Source:** [AWS Certified Solutions Architect - Associate (Subscription - Partner Subscription)](https://explore.skillbuilder.aws/learn/learning-plans/2159/aws-certified-solutions-architect-associate-subscription-partner-subscription), AWS Training & Certification.