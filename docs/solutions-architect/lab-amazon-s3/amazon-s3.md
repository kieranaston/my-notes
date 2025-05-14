# Introduction to Amazon Simple Storage Service (S3)

Say you want to have an S3 bucket that your EC2 instance can read and write to.

## Creating a bucket

1. Go to the S3 services page.
2. Choose "create bucket"
3. Names the bucket. Names can only have lowercase letters, numbers, or hyphens and must be globally unique
4. Configure other settings, create the bucket

## Adding files to the bucket

Can click on bucket, hit upload, and add files from your local machine to the bucket.

## Security of our bucket

Before connecting to EC2 instance, we want to check the security of the bucket to make sure everything is good.

We want to configure permissions and test the bucket and object settings.

To check that our bucket object is private we could try to access it by clocking on the object URL, and if we are denied access we know that the object is in face private.

If we try to make an individual object public it will block out access because by default, Block Public Access will be turned on for the bucket.

To change this, we go back to the main bucket page and navigate to the permissions tab. We deselect the block all public access option, and leave the others deselected as well.

These permissions are not very restrictive and not best practices, but just for the purposes of this lab they are fine.

Now we can navigate to the specific object once again and make it public via ACL.

If we wish to grant access to an entire bucket rather than just one specific object, we need to use bucket policies, covered later on.

## Testing connectivity to EC2 instance

We can connect to the instance like we did previously using Session Manager.

We can list all of our S3 buckets from the home directory using the command `aws s3 ls`.

To list all the objects in a specific bucket we can do: `aws s3 ls s3://nameofbucket`

Right now we are unable to copy files to the S3 bucket.

We can head to the roles page within the IAM section, search for EC2InstanceProfileRole. This is the Role that the EC2 instance uses to connect to S3.

Just as a reminder, IAM Roles define a set of permissions for users that are assumed temporarily.

We copy the role ARN here: arn:aws:iam::319196556365:role/EC2InstanceProfileRole

The ARN uniquely identifies AWS resources across all of AWS.

We now navigate to the bucket permissions and find the bucket ARN: arn:aws:s3:::reportbucket28239482390

Now, to create an S3 bucket policy, we can use the AWS Policy Generator.

PutObject is for uploads to S3 and GetObject is for retrieving files from S3.

## Versioning for buckets

versioning is a way to keep multiple variants of an object in the same bucket. You can preserve, retrieve, and restore every version of every object stored in your Amazon S3 bucket.

With versioning you can easily recover from both unintended user actions and application failures.

Versioning is enabled by the bucket and not for individual objects.

If files with the same name are uploaded, Amazon S3 always returns the latest version unless otherwise specified.

You can view and access previous versions with the S3 Management Console when looking within your bucket, however, you need to alter your policy to include "s3:GetObjectVersion" to access the older version.

When you delete an object that has versioning, a delete marker remains. When you permanently delete the delete marker, it effectively restores the object to its previous state.

However, when deleting a specific version of an object no delete marker is created and the object is permanently deleted.

## Important points from this lab

In an SIn an Amazon S3 bucket policy, which element specifies the AWS accounts or users that the policy applies to? Principal.

What is the primary purpose of Amazon S3 bucket versioning? To preserve, retrieve, and restore every version of every object in a bucket

What happens when you upload an object with the same name as an existing object in an S3 bucket? A new version is created if versioning is enabled, but otherwise the existing object is overwritten.

What happens if you try to create an Amazon S3 bucket with a name that already exists? The bucket creation fails, and you receive an error message

What is the default access setting for newly created S3 buckets? Private

**Source:** [AWS Certified Solutions Architect - Associate (Subscription - Partner Subscription)](https://explore.skillbuilder.aws/learn/learning-plans/2159/aws-certified-solutions-architect-associate-subscription-partner-subscription), AWS Training & Certification.