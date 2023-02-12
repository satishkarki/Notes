# IP Address

### Classful IP Address

Classful IP addresses are an outdated method of allocating IP addresses in computer networks. In the classful IP addressing system, IP addresses were divided into five classes (A, B, C, D, and E), each with a different number of bits for the network prefix and host suffix. The network prefix specified the network address, and the host suffix specified the individual host addresses within that network.

Class A addresses used 8 bits for the network prefix and 24 bits for the host suffix, allowing for 126 total networks and over 16 million hosts per network. Class B addresses used 16 bits for the network prefix and 16 bits for the host suffix, allowing for 16,384 total networks and up to 65,534 hosts per network. Class C addresses used 24 bits for the network prefix and 8 bits for the host suffix, allowing for 2,097,152 total networks and up to 254 hosts per network.

The classful IP addressing system was replaced with the Classless Inter-Domain Routing (CIDR) system, which allows for more efficient and flexible allocation of IP addresses by specifying a variable-length network prefix.

Note: Class D and Class E addresses are used for special purposes and are not assigned to host computers.



### Class D IP Address

Class D IP addresses are a range of IP addresses that are reserved for use in multicast applications. A multicast is a way of sending a single packet to multiple recipients simultaneously, which can be more efficient than sending individual packets to each recipient.

In the classful IP addressing system, Class D IP addresses were designated for use in multicast applications and had a range of IP addresses from 224.0.0.0 to 239.255.255.255. When a packet is sent to a Class D IP address, it is transmitted to all hosts that have joined the multicast group associated with that IP address.

Multicast is used in a variety of applications, such as video streaming, online gaming, and real-time collaboration. By using multicast, network traffic can be reduced and the efficiency of network communication can be improved.

It's important to note that Class D IP addresses are no longer used in modern IP addressing and have been replaced by Classless Inter-Domain Routing (CIDR) system, which provides more efficient and flexible allocation of IP addresses for both unicast and multicast applications.



### Private IP Address

Private IP addresses are a set of IP addresses that are reserved for use within private networks and are not routable on the public internet. Private IP addresses are used to assign addresses to devices within a private network, such as a home or office network.

The most commonly used private IP address ranges are:

- 10.0.0.0 to 10.255.255.255
- 172.16.0.0 to 172.31.255.255
- 192.168.0.0 to 192.168.255.255

These private IP addresses are not assigned to any specific organization, so multiple private networks can use the same private IP addresses. When devices within a private network communicate with each other, they use the private IP addresses assigned to them. When they need to communicate with the public internet, they use a network address translation (NAT) device, such as a router, which maps the private IP addresses to a public IP address.

The use of private IP addresses provides a level of security and protection for devices within a private network by hiding them from the public internet and making it more difficult for unauthorized users to access them directly. It also conserves the limited number of public IP addresses that are available for use on the public internet.