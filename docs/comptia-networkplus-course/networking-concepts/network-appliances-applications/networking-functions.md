# Networking functions

## Content delivery network (CDN)

Designed to provide way to get data very efficiently from one central point to a user. Often set up in different geographical regions. Able to cache data at each of these points.

## VPN

Connect to remote network while sending all data encrypted across this network. Very secure way to transfer data even across networks that would be inherently insecure.

## Quality of service (QoS)

Not all applications designed to run simulateneously on organization's network and some might have higher priority. Very common for network administrators to provide some sort of prioritization for these applicatons. Often through QoS configuration.

Usually based on bandwidth usage or particular data frames. This might be managed through firewall, router, or switch.

## Time ot live (TTL)

Can sometimes end up with devices doing something or tryingto do something over and over again without ever completing it, need to manage/mitigate this. Can recognize this and remove it from network if this happens.

TTL is some type of timer, once it hits zero we can drop a task from network or have it stop what it's doing. One common use is stopping router loops.

## IP (internet protocol)

Loops could cause a packet to live forever, so sometimes we need to drop a packet after a certain number of hops (each pass through a router is a hop). A normal number of hopes is around 12, and the limit for Mac and Windows is 64 and 128, respectively.

## DNS (domain name system)

In DNS, time to live associated with total number of seconds. A device caches the lookup for a certain number of time. 