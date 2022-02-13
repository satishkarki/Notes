##  IPv4 and IPv6 Addresses

IPv4 has 32 bits i.e 4 octets where as IPv6 has 128 bits.

| 128  | 64   | 32   | 16   | 8    | 4    | 2    | 1    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |

### IPv4 Address Structure

| Dotted Decimal Notation      | 10                      | 1                    | 2                    | 3                    |
| ---------------------------- | ----------------------- | -------------------- | -------------------- | -------------------- |
| Binary Bits                  | 00001010 Octet1         | 00000001 Octet2      | 00000010 Octet3      | 00000011 Octet4      |
| Subnet Mask                  | 11111111 (network bits) | 00000000 (host bits) | 00000000 (host bits) | 00000000 (host bits) |
| Network Address              | 10                      | 0                    | 0                    | 0                    |
| Network Address(binary bits) | 00001010                | 00000000             | 00000000             | 00000000             |

`Subnet Mask`: The IP address component that determines which bits represent the network and which bits represent the host 

Prefix Notation: 10.1.2.3/8

### **Classes of Addresses**

| Address Class | Value in First Octet | Classful Mask(Dotted Decimal) | Classful Mask(Prefix Notation) |
| ------------- | -------------------- | ----------------------------- | ------------------------------ |
| Class A       | 1-126                | 255.0.0.0                     | /8                             |
| Class B       | 128-191              | 255.255.0.0                   | /16                            |
| Class C       | 192-223              | 255.255.255.0                 | /24                            |
| Class D       | 224-239              | -                             | -                              |
| Class E       | 240-255              | -                             | -                              |

Note: The reason is that 127 is used as a loopback IP address, meaning a locally significant IP address representing the device itself.



**Private IP Address**

| Address Class | Address Range                  | Default Subnet Mask |
| ------------- | ------------------------------ | ------------------- |
| Class A       | 10.0.0.0 - 10.255.255.255      | 255.0.0.0           |
| Class B       | 172.16.0.0 - 172.31.255.255    | 255.255.0.0         |
| Class B       | 169.254.0.0 - -169.254.255.255 | 255.255.0.0         |
| Class C       | 192.168.0.0 - 192.168.255.255  | 255.255.255.0       |

Note: The 169.254.0.0–169.254.255.255 address range is not routable. Addresses in the range are only usable on their local subnet and are dynamically assigned to network hosts using the Automatic Private IP Addressing (APIPA) feature.



**Types of Addresses**

Unicast: traffic travels from a single source device to a single destination device

Broadcast: traffic travels from a single source device to all the destination on a network(that is a broadcast domain)

Multicast: traffic travels from a single source device to many but specific devices. A Class D address, such as 239.1.2.3, represents the address of a multicast group. Example, a video server



**Assigning IPv4 Address**

default gateway: if traffic is destined for a different subnet than the subnet on which the
traffic originates, a default gateway needs to be defined

- Static Configuration
- Bootstrap protocol (BOOTP) used in early days, BOOTP broadcast was sent out from the device needing the IP address and Bootstrap Server would provide the IP address
- DHCP provides IP address and DNS server automatically
- Automatic Private IP Addressing (APIPA)

### Subnetting

```bash
Number of assignable IP addresses in a subnet = 2^h – 2,
where h is the number of host bits in a subnet mask
```

Assignable IP Address



| Address Class | Assignable IP Address |
| ------------- | --------------------- |
| Class A       | 16,777,214 (2^24 –2)  |
| Class B       | 65,534 (2^16 –2)      |
| Class C       | 254 (2^8 –2)          |

**Subnet Octet Values**

| Number | Subnet octet value | Number of Contiguous Left-Justified One |
| ------ | ------------------ | --------------------------------------- |
| 1      | 255                | 8                                       |
| 2      | 254                | 7                                       |
| 4      | 252                | 6                                       |
| 8      | 248                | 5                                       |
| 16     | 240                | 4                                       |
| 32     | 224                | 3                                       |
| 64     | 192                | 2                                       |
| 128    | 128                | 1                                       |

**Dotted-Decimal and Prefix-Notation Representations for IPv4 Subnets**

| Dotted-Decimal Notation | Prefix Notation                                 |
| ----------------------- | ----------------------------------------------- |
| 255.0.0.0               | /8 (Classful subnet mask for Class A networks)  |
| 255.128.0.0             | /9                                              |
| 255.192.0.0             | /10                                             |
| 255.224.0.0             | /11                                             |
| 255.240.0.0             | /12                                             |
| 255.248.0.0             | /13                                             |
| 255.252.0.0             | /14                                             |
| 255.254.0.0             | /15                                             |
| 255.255.0.0             | /16 (Classful subnet mask for Class B networks) |
| 255.255.128.0           | /17                                             |
| 255.255.192.0           | /18                                             |
| 255.255.224.0           | /19                                             |
| 255.255.240.0           | /20                                             |
| 255.255.248.0           | /21                                             |
| 255.255.252.0           | /22                                             |
| 255.255.254.0           | /23                                             |
| 255.255.255.0           | /24 (Classful subnet mask for Class C network)  |
| 255.255.255.128         | /25                                             |
| 255.255.255.192         | /26                                             |
| 255.255.255.224         | /27                                             |
| 255.255.255.240         | /28                                             |
| 255.255.255.248         | /29                                             |
| 255.255.255.252         | /30                                             |

**Burrowed Bits**

To determine the number of subnets created when adding bits to a classful mask, you can use the following formula:

```
Number of created subnets = 2^s
where s is the number of borrowed bits
```

let’s say you subnetted the 192.168.1.0 network with a 28-bit subnet mask, and you want to determine how many subnets were created. 192.168.1.0 is Class C network i.e /24 which means:

```
Number of borrowed bits = Bits in custom subnet mask – Bits in classful subnet mask
Number of borrowed bits = 28 – 24 = 4
```

From this calculation, you conclude that subnetting 192.168.1.0/24 with a 28-bit subnet mask yields 16 subnets.



**Calculating the Number of Available Hosts**

```
Number of assignable IP address in a subnet = 2^h – 2
where h is the number of host bits in the subnet mask
```

let’s say you want to determine the number of available host IP addresses in one of the 192.168.1.0/28 subnets.

```
Number of host bits = 32 – Number of bits in subnet mask
Number of host bits = 32 – 28 = 4
```

From this calculation, you can conclude that each of the 192.168.1.0/28 subnets has 14 usable IP addresses.



**Calculating New IP Address Range**

A 27-bit subnet mask is applied to a network address of 192.168.10.0/24. To calculate the created subnets, you can perform the following steps:

```bash
Step 1. The subnet mask /27 (in binary) is 11111111.11111111.11111111.11100000. The interesting octet is the fourth octet because the fourth octet contains the last 1 in the subnet mask.

Step 2. The decimal value of the fourth octet in the subnet mask is 224 (11100000 in decimal). Therefore, the block size is 32 (256 – 224 = 32).

Step 3. The first subnet is 192.168.10.0/27—the value of the original 192.168.10.0 network with the borrowed bits (the first three bits in the fourth octet) set to 0.

Step 4. Counting by 32 (the block size) in the interesting octet (the fourth octet) allows you to calculate the remaining subnets:
192.168.10.0
192.168.10.32
192.168.10.64
192.168.10.96
192.168.10.128
192.168.10.160
192.168.10.192
192.168.10.224

The next logical step is to determine the usable addresses within those subnets.
# You cannot assign an IP address to a device if all the host bits in the IP address are set to 0, because an IP address with all host bits set to 0 is the address of the subnet itself.
# Similarly, you cannot assign an IP address to a device if all the host bits in the IP address are set to 1 because an IP address with all host bits set to 1 is the directed broadcast address of a subnet.

```

By excluding the network and directed broadcast addresses from the 192.168.10.0/27 subnets (as previously calculated), the usable addresses shown in the table:

| Subnet Address | Directed Broadcast Address | Usable IP Addresses           |
| -------------- | -------------------------- | ----------------------------- |
| 192.168.10.0   | 192.168.10.31              | 192.168.10.1–192.168.10.30    |
| 192.168.10.32  | 192.168.10.63              | 192.168.10.33–192.168.10.62   |
| 192.168.10.64  | 192.168.10.95              | 192.168.10.65–192.168.10.94   |
| 192.168.10.96  | 192.168.10.127             | 192.168.10.97–192.168.10.126  |
| 192.168.10.128 | 192.168.10.159             | 192.168.10.129–192.168.10.158 |
| 192.168.10.160 | 192.168.10.191             | 192.168.10.161–192.168.10.190 |

**Classless Interdomain Routing**

Whereas subnetting is the process of extending a classful subnet mask (that is, adding 1s to a classful mask), classless interdomain routing (CIDR) does just the opposite. Specifically, CIDR shortens a classful subnet mask by removing 1s from the classful mask. As a result, CIDR allows contiguous classful networks to be aggregated. This process is sometimes called `route aggregation`.

### IP version 6

IPv6 offers approximately 5*10^28 IP addresses for each person on the planet.

Beyond the increased address space, IPv6 offers many other features:
	Simplified header:
		IPv4 header uses 12 fields.
		IPv6 header uses five fields.
	No broadcasts.
	No fragmentation (performs MTU discovery for each session).
	Can coexist with IPv4 during a transition.
		Dual stack (running IPv4 and IPv6 simultaneously on a network interface or device).
		IPv6 over IPv4 (tunneling IPv6 over an IPv4 tunnel).

**IPv6 Address Structure**

```bash
XXXX:XXXX:XXXX:XXXX:XXXX:XXXX:XXXX:XXXX
# X= a hexadecimal digit in the range of 0 to F
# hexadecimal digit is 4 bits in size
# 4 bits per digit * 4 digits per field * 8 fields = 128 bits in an IPv6 address
```

Rules:

```bash
#Leading 0s in a field can be omitted.

#Contiguous fields containing all 0s can be represented with a double colon.(Note that this can be done only once for a single IPv6 address.)

ABCD:0123:4040:0000:0000:0000:000A:000B
ABCD:123:4040::A:B
```

**IPv6 Address Type**

- IPv6 globally routable unicast addresses start with the first four hex characters in the range of 2000 to 3999.
- An IPv6 link-local address is also used on each IPv6 interface. The link-local address begins with FE80.
- Multicast addresses begin with FF as the first two hex characters.
- IPv6 can use autoconfiguration to discover the current network and select a host ID that is unique on that network. Automatic generation of a unique host ID is made possible through a process known as EUI64, which uses the 48-bit MAC address on the device to aid in the generation of the unique 64-bit host ID. Notice that the autoconfiguration capabilities described here permit you to create an IPv6 network free of DHCP-type services.
- IPv6 can also use a special version of DHCP for IPv6. Not surprisingly, this version is called DHCPv6.
- The protocol that is used to discover the network address and learn the Layer 2 address of neighbors on the same network is Neighbor Discovery Protocol (NDP).

**Neighbour Discovery Protocol** 

similar to the ARP. 

NDP defines five ICMPv6 packet types for important jobs.

The **Internet Control Message Protocol** (**ICMP**) is a supporting [protocol](https://en.wikipedia.org/wiki/Communications_protocol) in the [Internet protocol suite](https://en.wikipedia.org/wiki/Internet_protocol_suite). It is used by [network devices](https://en.wikipedia.org/wiki/Network_device), including [routers](https://en.wikipedia.org/wiki/Router_(computing)), to send error messages and operational information indicating success or failure when communicating with another [IP address](https://en.wikipedia.org/wiki/IP_address), for example, when an error is indicated when a requested service is not available or that a [host](https://en.wikipedia.org/wiki/Host_(network)) or router could not be reached.

- **Router Solicitations**: The ICMP Router Solicitation message is sent from a computer host to any routers on the local area network to request that they advertise their presence on the network. 
- **Router Advertisement**: Routers advertise their presence together with various link and Internet parameters, either periodically or in response to a Router Solicitation message.
- **Neighbour Solicitation**: Neighbor solicitations are used by nodes to determine the link layer address of a neighbor, or to verify that a neighbor is still reachable via a cached link layer address.
- **Neighbour Advertisement**: Neighbor advertisements are used by nodes to respond to a Neighbor Solicitation message.
- **Redirect**: Routers may inform hosts of a better first-hop router for a destination.

**IPv6 Data Flow**

- Unicast
- Multicast
- Anycast

