# Security policies

Identity-based policies and resource-based policies grant permissions to allow or deny actions. You define the permission of a principal (person) or resource.

IAM permission boundaries and AWS service control policies (SCPs) are used to set boundaries in an organization to set upper boundaries. Broad approach, defining maximum permissions for an IAM user or group.

IAM identity-based policies are assigned to users, groups, and roles, while IAM resource-based policies are assigned to resources.

Resource-based policies also include a principal that controls what someone is allowed to do with that resource.

## Identity-based policies

Can be managed or inline. Managed are managed by AWS or customer.

Inline policies are one-to-one with a single user, group, or role.

## Resource-based policies

Inline policies for resources.

Grant permission to the principal specified in the policy to access resources.

Principals can be in the same account as the resource or other accounts.

## Permission boundaries

Can use a managed policy as the permissions boundary for a user or role, and them no identity-based policy can grant permissions past that permission boundary.

## AWS organizations service control policies

Can use service control policies to set maximum permissions for account members or organization or organizational unit.

## Access control lists (ACLs)

Control which principals in other accounts can access a resource to which the ACL is attached.

Similar to resource-based policies. Only policy type not using the JSON structure.

## Defense in depth

Strategy with goal of having multiple layers of security. Involves having multiple security controls at every layer of a request.

## Components of a policy

Effect: What is the policy doing? Allowing or denying?

Principal: Account, user, or role that the policy applies to.

Action: What actions are we applying this effect to?

Resource: Which resources does this policy apply to?

Condition: Conditions for the policy to apply.

## How IAM policies are evaluated

First checks if action is explicitly denied.

Then checks if action is explicitly allowed.

If it is, then it allows the action to be performed.

If not, then it denies the action.

**Source:** [AWS Certified Solutions Architect - Associate (Subscription - Partner Subscription)](https://explore.skillbuilder.aws/learn/learning-plans/2159/aws-certified-solutions-architect-associate-subscription-partner-subscription), AWS Training & Certification.