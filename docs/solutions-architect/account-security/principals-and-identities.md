# Principals and identities

The principal is who is performing an action in AWS.

## AWS account root user

Can do anything, like root user in Linux operating system. Should not generally be used for day-to-day interactions.

## Identity and access management (IAM)

Web service for controlling access to your AWS resources.

This is the tool for managing all types of access to your resources in one place, with fine control over permissions. This helps you define who has permissions to which API calls

The place where we do authentication and authorization. Authentication is proving that I am who I say I am.

## Principals

Principal can make a request for an action or operation on an AWS resource. Can be a person, application, federated user, or assumed role.

## IAM users

Have credentials and permissions. Policies can be attached to them to control what they can do.

## How do IAM users make API calls and how are they restricted?

So they can do stuff through the AWS Management Console, just with a password.

They can also access programmatically, using the AWS CLI (you can install this to your computer) or AWS SDKs (development kits for using AWS services through popular programming languages).

These programmatic options use access key IDs and secret keys.

## Setting permissions with IAM policies

You can define your own policies and apply them to IAM users.

We apply the principle of least privilege when defining policies.

## IAM user groups

Can also apply policies to a group rather than just a user. So these are IAM user groups. Users can inherit permissions from these groups.

## IAM roles

Roles delegate set permissions to certain users of services.

This is good for giving someone permissions for a short period of time, because these permissions are valid only while the role is active.

## Assuming a role

So you can use an API call to assume a role, this returns temporary credentials that you can use for a period of time.

## IAM policy assignments

Assigned to IAM users, groups, roles. Role is assumed. IAM user can assume a role, AWS resource itself can assume a role because it needs to perform a certain action within AWS.

**Source:** [AWS Certified Solutions Architect - Associate (Subscription - Partner Subscription)](https://explore.skillbuilder.aws/learn/learning-plans/2159/aws-certified-solutions-architect-associate-subscription-partner-subscription), AWS Training & Certification.