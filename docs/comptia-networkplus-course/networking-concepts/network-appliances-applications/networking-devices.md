# Networking devices

## Router

Allows us to take data on one IP subnet and route that info to a different IP subnet.

OSI layer 3 (network layer) device. At this layer we are referring to IP addresses, and this is what is used by routers to be able to determine next hop for this information.

These routers often connect many different types of networks (LAN, WAN, copper, fiber).

## Switch

Operate at MAC address layer (layer 2, data link layer) to be able to forward traffic. These operate mostly in hardware.

## Security

Filter traffic by port number or application depending on traditional or newer firewall. Can also encrypt traffic (VPN between sites). Most firewalls can operate as layer 3 devices (routers). We rely on firewall to manage communication between inside and outside of the network.

## IDS and IPS

Intrusion Detection System / Intrusion Prevention System. Many data centers have these standalone systems to watch network traffic. A lot of this functionality is integrated into modern next-generation firewalls, though. Looking for attacks inbound to your network and are able to identify, alert, and a lot of the time to prevent them from gaining access to your network.

Intrusion prevention system is able to block particular attack before it gets inside your network, unlike intrusion detection system which detects threats that have already gotten inside.

## Load balancer

High traffic sites can use a load balancer to distribute the load across multiple physical servers. Load balancers also very good at identifying outages to these servers. The load balancer can also handle the encryption and caching of data. Can also perform prioritization of traffic with the load balancer.

## Proxies

Sits between the users and the external network. Often security concerns with individual users communicating directly with server or service that is on the internet. One of the ways this can be managed is by putting a proxy in the middle of the conversation.

Responsible for taking the user's request, performing it on their behalf and receiving the answer, verifying it is not malicious, and providing it back to user.

Since it sits in middle of conversation it is perfect place to do caching.

## NAS vs. SAN

Very commo nto store documents and other files on centralized storage facilities inside of our data centers. Network-attached storage (NAS) provides file-level access (if we want info from a file we have to pull over the entire file across the network into our system, and when writing info to that file we write the entire file back to the NAS). A storage area network (SAN) is very similar to reading and writing information from a local storage drive but instead of copying entire file to change just a bit of information within it we have block-level access, which means that we can change just the blocks that have been modified. Is much more efficient for very large files.

Common to put a NAS or SAN on a very high-bandwidth network on its own to support lots of file transfers to these systems.

## Access point (AP)

Allows us to communicate wirelessly from our device to the rest of the network. Not a wireless router, which is a router, and access point, and switch in same device.

This bridges communication between the wireless network and the wired ethernet network. This is why they are referred to as OSI layer 2 devices (data link layer).

## Wireless LAN controllers

There might be access points that we need to manage across many different locations. Instead of connecting to each individual access point every time we want to make configuration changes or manage these processes, we can have a centralized management tool allowing us to manage all of our access points from one central place. Wireless LAN controllers give us a single pane of glass so that we can manage the entire infrastructure while we're sitting in one chair.

Can deploy new access points with full configuration, could set up performance and security monitoring, and can automatically deploy changes to all access points easily. Can also easily create reports on usage of access points.

Often use wireless LAN controllers form same manufacturer as access points (proprietary systems).