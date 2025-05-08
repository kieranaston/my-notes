# IP addressing

When you see an IP address slash something, it means we are representing a range of IP addresses.

The bigger this number, the smaller the network is.

The start identifies the network, the middle identifies the host, and the end identifies the range.

## IPv4 addresses

32-bit addresses. Bits grouped in four sets of 8 bits called octets.

First two octets identify network, last two designate the resource within the network.

## IPv6 addresses

128-bit addresses. Eight groups of four hexadecimal digits with colon as separator.

## Classless inter-domain routing (CIDR)

Method of assigning IP addresses improving efficiency of address distribution.

Addresses specified in CIDR block.

By default all VPCs and subnets need to have IPc4 CIDR blocks.

Identifies network using dot notation and subnet mask using slash notation.

## AWS supported CIDR ranges

Network can be identified using 16-28 bits in 32 bit IPv4 address. Resources in subnet can be identified using 4-16 bits in 32 bit IPv4 address. 