# Designing the cloud

## Key characteristics of the cloud

Can easily deploy application and services with seemingly unlimited resources. Able to scale up and down these applications as needed, providing elasticity.

Also can access these applications from anywhere in world. Also multi-tenancy, many customers using same cloud infrastructure. This makes for efficiency in use of technology and how much it costs.

## Virtual networks

Can not only have virtual servers living in cloud but can also have virtual networks. Can run 100 virtual servers inside one large physical server instead of 100 different physical servers.

## Network function virtualization (NFV)

Virtualize network infrastructure as well, reaplce routers, switches, and other network devices with virtual versions of them. Same functionality, now in virtual appliance.

Just as we are able to easily deploy a new server, we can do the same with our switches, firewalls, routers, etc. from the hypervisor.

A lot of flexibility for deploying applications, deisgning network connectivity for those applications, and connecting our different cloud infrastructures wherever they might be in the world.

## Connecting to the cloud

All of our virtual devices could be run in a Virtual Private Cloud (VPC). Common to have separate VPCs for different application instances and/or parts of company.

We use a transit gateway to be able to connect all the VPCs together. Can think of it as a "cloud router" that allows us to connect and allow communication between all of our VPCs.

Might commonly use a VPN to connect to these private VPCs.

## Security groups and lists

Many cloud providers will include additional security that you can layer on top of your VPCs. These allow us to control inbound and outbound traffic to your VPCs.

This is very similar to configuring a traditional firewall.

## Network security list

In cloud provider's frontend you would include in your network security list the list of rules you would like to assign.

Once you apply your network security list it will be applied to all your virtual private clouds.

## Network security group

Used to assign a security rule to a specfic virtual NIC (VNIC). Applies to specific devices and network connections.

This improves granularity.

