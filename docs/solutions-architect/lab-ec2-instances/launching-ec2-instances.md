# Launching EC2 instances

## EC2 page

From the AWS Management Console, there is a search bar you can use to navigate to the pages for different services.

The EC2 page is all about EC2s, and contains info for the particular region that is selected. You can of course launch instances from this page.

## Service Quotas page

The service quotas page has info on service quota (limits) for various services. It is possible to request a service quota increase.

## AMI Catalog

The AMI catalog is the page for AMIs (Amazon Machine Image). AMIs are basically EC2 configurations specifying operating system, application server, applications, etc. that can be used to launch pre-configured EC2 instances.

Basically a way to store your environment configuration.

Found under the images section of the sidebar on the EC2 page because they are essentially snapshots of a system's state.

## To launch an EC2 instance...

1. Name it
2. Select AMI or configure it yourself
3. Select the instance type
4. Select the key pair
5. Select the VPC (default is fine too)
6. Hit "launch instance"

You can review the instance by heading to the "view all instances" page.

At first it will be pending, but once it is running you can connect to it and use it in the same way that you'd use a computer in front of you.

## Instance states

When you stop and start your instance, you lose any data in the instance store. However, you retain its private IPv4 address, meaning that an Elastic IP address associated with the private IPv4 address or network interface is still associated with your instance.

The significance of retaining the IP is that every component of your architecture that could be reliant on IP is not disrupted.

You can also reboot your instance. It remains on the same computer and this does not disrupt the instance store or anything like that. Same as rebooting an operating system.

Instance can also be put into hibernation, saving the contents from the instance memory to your EBS root volume. The instance's Amazon EBS root volume and any attacked Amazon EBS data volumes persist. Other stuff like IP is also retained.

Instance termination is when you no longer need an instance. It remains on the console for a bit then the entry is automatically deleted.

## Instance details

To review instance details you click on the "actions" dropdown and choose "view details". This shows you a summary of the instance's attributes like addresses, state, type, etc.

## Runing commands when you launch an EC2 instance with user data input

You can actually include a shell script in the "user data" field that will be run when the EC2 instance is launched. In the tutorial this was used to get a basic web application up and running.

## Accessing an EC2 instance

Can use Session Manager to connect to an instance. This allows you to manage your instance with a CLI.

If you plan to connect to your instance using SSH, you must specify a key pair. Essentially when the instance boots for the first time that key is stored on the virtual machine, and when you connect to your Linux instance using SSH you must specify the private key corresponding to that public key stored on the VM.

You can now navigate the EC2 instance (Linux VM) as if it was just a CLI on a Linux machine.

## Instance types

Different instance types like t3.small and t3.micro represent different hardware configurations.

## Modifying storage volumes

1. Go to actions -> view details
2. Go to storage
3. Go to block devices section
4. Click on the volume ID for the root device
5. On the volumes page select the volume
6. Choose actions -> modify

You can change the volume type and the size.

When an EBS volume is modified it goes through a series of states, and this process might take some time.

**Source:** [AWS Certified Solutions Architect - Associate (Subscription - Partner Subscription)](https://explore.skillbuilder.aws/learn/learning-plans/2159/aws-certified-solutions-architect-associate-subscription-partner-subscription), AWS Training & Certification.