## Ethernet Technology

**CSMA/CD**

The procedure used by Ethernet to decide whether it is safe to transmit, detect collisions, and re transmit if necessary is called carrier-sense multiple access/collision detection (CSMA/CD). 

Components: Carrier Sense, Multiple Access and Collision Detection



**Distance and Speed Limitations**

The bandwidth of a network is measured in terms of how many bits the network can transmit during a 1-second period of time. 

| Ethernet Type        | Bandwidth Capacity                                           |
| -------------------- | ------------------------------------------------------------ |
| Standard Ethernet    | 10Mbps: 10 million bits per second (that is, 10 megabits per second) |
| Fast Ethernet        | 100Mbps: 100 million bits per second (that is, 100 megabits per second) |
| Gigabit Ethernet     | 1Gbps: 1 billion bits per second (that is, 1 gigabit per second) |
| 10-Gigabit Ethernet  | 10Gbps: 10 billion bits per second (that is, 10 gigabits per second) |
| 100-Gigabit Ethernet | 100Gbps: 100 billion bits per second (that is, 100 gigabits per second) |

**Types of Ethernet**

| Ethernet Standard | Media Type            | Bandwidth Capacity | Distance Limitation |
| ----------------- | --------------------- | ------------------ | ------------------- |
| 10BASE5           | Coax(thicknet)        | 10Mbps             | 500 m               |
| 10BASE2           | Coax(thinnet)         | 10Mbps             | 185 m               |
| 10BASE-T          | CAT3 (or higher) UTP  | 10Mbps             | 100 m               |
| 100BASE-TX        | CAT5 (or higher) UTP  | 100Mbps            | 100 m               |
| 100BASE-FX        | MMF                   | 100Mbps            | 2 km                |
| 1000BASE-T        | Cat 5e(or higher) UTP | 1Gps               | 100 m               |
| 1000BASE-TX       | Cat 6 (or higher) UTP | 1Gps               | 100 m               |

**Ethernet Switch Features**

- VLAN
  - Logically divide switch into different broadcast domain

- Switch Configuration for Access Point
  - Trunks:The most popular trunking standard today is IEEE 802.1Q, which is often referred
    to as `dot1q`
  
- Spanning Tree Protocol (STP)

  - STP allows the network to physically have Layer 2 loop but strategically blocks data from flowing over one or two switches to prevent looping of traffic
  - STP prevents corruption of a switch's MAC addresses table
  -  IT also prevents `Broadcast storm`

- STP Operation

  Root Bridge Election

  ![Root Bridge Election	](https://images2.imgbox.com/b6/f1/Uz3IvYXR_o.png)

- `Root bridge`: A switch elected to act as a reference point for a spanning tree.
  The switch with the lowest bridge ID (BID) is elected as the root bridge. The
  BID is made up of a priority value and a MAC address.

- `Nonroot bridge`: All other switches in the STP topology are nonroot bridges.

STP Port Type



![](https://images2.imgbox.com/c9/76/lRNnnSFE_o.png)

| Port Type           | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| Root Port           | Every non root bridge has a single root port, which is the port on that switch that is closest to the root bridge in terms of cost. |
| Designated Port     | Every network segment has a single designated port, which is the port on that segment that is closest to the root bridge in terms of cost. Therefore, all ports on a root bridge are designated ports. |
| Non-designated Port | Non designated ports block traffic to create a loop-free topology. |

STP Port Cost



![](https://images2.imgbox.com/c9/76/lRNnnSFE_o.png)



| Link Speed                   | STP Port Cost |
| ---------------------------- | ------------- |
| 10Mbps (Ethernet)            | 100           |
| 100Mbps (Fast Ethernet)      | 19            |
| 1Gbps (Gigabit Ethernet)     | 4             |
| 10Gbps (10-Gigabit Ethernet) | 2             |



**Bridge Protocol Data Units** (BPDUs) are [frames](https://en.wikipedia.org/wiki/Frame_(networking)) that contain information about the [spanning tree protocol](https://en.wikipedia.org/wiki/Spanning_tree_protocol) (STP). A switch sends BPDUs using a unique source [MAC address](https://en.wikipedia.org/wiki/MAC_address) from its origin [port](https://en.wikipedia.org/wiki/Port_(computer_networking)) to a [multicast address](https://en.wikipedia.org/wiki/Multicast_address) with destination MAC (01:80:C2:00:00:00,[[1\]](https://en.wikipedia.org/wiki/Bridge_Protocol_Data_Unit#cite_note-1) or 01:00:0C:CC:CC:CD for [Cisco proprietary Per VLAN Spanning Tree](https://en.wikipedia.org/wiki/Spanning_Tree_Protocol#Per-VLAN_Spanning_Tree_and_Per-VLAN_Spanning_Tree_Plus)).[[2\]](https://en.wikipedia.org/wiki/Bridge_Protocol_Data_Unit#cite_note-2)

There are two kinds of BPDUs for 802.1D Spanning Tree:[[3\]](https://en.wikipedia.org/wiki/Bridge_Protocol_Data_Unit#cite_note-3)

- Configuration BPDU, sent by root bridges to provide information to all switches.
- TCN (Topology Change Notification), sent by bridges towards the root bridge to notify changes in the topology, such as port up or port down.

By default the BPDUs are sent every 2 seconds.



If a nondesignated port needs to transition to the forwarding state, it does not do so
immediately. Rather, it transitions through the following states:



- `Blocking`: The port remains in the blocking state for 20 seconds by default.
  During this time, the nondesignated port evaluates BPDUs in an attempt to
  determine its role in the spanning tree.
- `Listening`: The port moves from the blocking state to the listening state and
  remains in this state for 15 seconds by default. During this time, the port
  sources BPDUs, which inform adjacent switches of the port’s intent to forward
  data.
- `Learning`: The port moves from the listening state to the learning state and
  remains in this state for 15 seconds by default. During this time, the port
  begins to add entries to its MAC address table.
- `Forwarding`: The port moves from the learning state to the forwarding state
  and begins to forward frames.

**Link Aggregation**

Suppose multiple devices are connected to a switch and all are operating at a speed of 100Mbps and the switch is  connected to another switch at operating at 100 Mbps. Then it will cause congestion at port connected to the other switch. The process of logically combining multiple physical connection into a single logical connection so that the traffic can pass to alleviate congestion is known as LA.

`LACP`: Link Aggregation Control Protocol

The `IEEE802.3ad `standard supports Link Aggregation Control Protocol (LACP).



**Power over Ethernet**

The switch feature that provides power to attached devices

`IEEE 802.3af` standard specifies 15.4W as the maximum amount of power a switch is allowed to provide per port.



**Port Monitoring**

Tools like WireShark can sniff the network. A network sniffer connected to a hub can monitor all the traffic. In case of the switch, port mirroring needs to be done in the switch in order to capture all traffic.



**User Authentication**

A standards-based method of enforcing user authentication is IEEE 802.1X.

- `Supplicant`: The device that wants to gain access to the network.
- `Authenticator`: The authenticator forwards the supplicant’s authentication request on to an authentication server. After the authentication server authenticates the supplicant, the authenticator receives a key that is used to communicate securely during a session with the supplicant.

- `Authentication server`: The authentication server (for example, a Remote Authentication Dial In User Service [RADIUS] server) checks a supplicant’s credentials. If the credentials are acceptable, the authentication server notifies the authenticator that the supplicant is allowed to communicate on the network. The authentication server also gives the authenticator a key that can be used to securely transmit data during the authenticator’s session with the supplicant.

**Management Band and Authentication**

`out-of-band` (OOB) management when the management traffic is kept on a separate network than the user traffic



