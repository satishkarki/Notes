

I am preparing for my CompTIA Network+ exam. And this is the first module of the many which I have noted down for the preparation purpose. This module covers the fundamentals of the network, OSI model and its difference with the TCP/IP stack model. At the end I have listed well known Internet Protocols with their ports. I am following the Cert Guide by Anthony Sequeira.

## Basic Terminology

The goal of this module is to acquaint you with the basic concept of network and  help you categories the network based upon the topology, geography and the location of network's resources. 

- `Converged Network`: A single network with the capacity to carry a combination of data, voice and video traffic.

- `Hub`: layer 1 device, doesn't perform inspection of traffic it passes, receives traffic at a port and repeats that traffic out all the other ports
- `Switch`: layer 2 device, inspects the traffic and forwards to the appropriate port, forwarding decision is based on the address which is physically burned into the NIC of the host (MAC address) 
- `Router`: layer 3 device, forwarding decision is based upon the logical IP address, when the traffic arrives, it looks for the destination IP  address of the traffic and based upon its database of network(routing table) it intelligently forwards the traffic to the appropriate interface
- `Media`: the medium to connect everything, could be a cable or wireless medium

## Network Defined by Connection

- LAN, WAN, WLAN, SAN, CAN, MAN, PAN

- `IEEE`: Institute of Electrical and Electronic Engineers

- Multi protocol Level Switching (MPLS) and Asynchronous Transfer Mode(ATM) are example of WAN
- The actual traffic flow determines the logical topology whereas the way components are physically connected determines the physical topology
- `Bus Topology`
  - network segment:  a bus and all devices connected to that bus
  - a single network segment is a single collision domain which means all the devices might try to access the bus at the same time which might result in collision
  - network components are connected directly to the cable by a T connector or vampire tap
- `Ring Topology`: Example- Fiber Distributed Data Interface(FDDI)
- `Star Topology`: Most popular LAN topology used today
- `Hub and Spook Topology`: Similar to the star topology of LAN but used in WAN, remote site is called spook site and main site is called hub site
- `Full Mesh Topology`: 
  - Directly connects every site to one another
  - The number of WAN connection `w=n*(n-1)/2` where w is the number of WAN and n is the number of sites
- `Partial Mesh Topology`: hybrid of full mesh and hub-spook topology
- `Wireless topology`:
  - `Ad HOC`: wireless P2P connection, Apple Airdrop
  - `Infrastructure`: Wireless LAN with Wireless Access Point (WAP). WAP connects to the Service Provider.
  - `Mesh`
- `Client/Server & Peer-to-peer`: based upon the location of the resources

## The OSI Model

The open system interconnection  model was developed as a way to help disparate computing systems communicate with each other. Most devices do function at more than one level of OSI reference model. When it comes time to determine where they fit in the model, you must first determine the highest level at which they operate. To do that you must know what they do and how that relates to the OSI Model.

`Please Do Not Throw Sausage Pizza Away` 

`All people Seems To Need Data Processing`

`Some People Fear Birthdays`

| Layer           | Data Type                      | Includes                            |
| --------------- | ------------------------------ | ----------------------------------- |
| 1. Physical     | Bits                           | Hub, Wireless Access Point, Cabling |
| 2. Data Link    | Frames                         | Switch, Bridges, NICs               |
| 3. Network      | Packets                        | Router                              |
| 4. Transport    | Segment                        | TCP UDP ICMP                        |
| 5. Session      |                                |                                     |
| 6. Presentation | Data Formatting and Encryption |                                     |
| 7. Application  |                                | Email, File Sharing                 |

`PDU`: Protocol Data Unit aka Packets or Data Service Unit, group of bits

### Layer 1 The Physical Layer

It defines the following:

- How bits are represented on the medium: current state modulation and state transition modulation, other modulations are AM and FM
- Wiring Standards for connectors and jacks
- Physical topology: It views network as a physical topology as opposed to logical topology
- Synchronizing bits: Synchronous(use of external clock) or Asynchronous(sending start and stop bits) communication
- Bandwidth usage: Broadband(divides bandwidth into different channel eg. Cable TV) and Baseband (uses all available frequencies eg: Ethernet)
- Multiplexing Strategy: allows multiple communication session to share the same physical medium
  - TDM Time Division Multiplexing
  - StatTDM Statistical Time Division multiplexing
  - FDM Frequency Division Multiplexing eg. Baseband (Ethernet)

### Layer 2 The Data Link Layer

<u>Data Link Control</u>

- Packaging Data into frames and transmitting those frames into the network
- Performing Error Detection and correction
- Uniquely finding network device with an address
- Handling flow control

<u>Sublayer</u>

1. **Media Access Control**

- Physical addressing

  | 7C   | A1   | AE   | 12   | 34   | 56   |
  | ---- | ---- | ---- | ---- | ---- | ---- |

  48 bit address assigned to to NIC

  First 24 bits represents the vendor code, last 24 bits assigned by the manufacturer

  Find the vendor code list [here](http://standards-oui.ieee.org/oui/oui.txt)

- Logical Topology: Level 2 views the network as a logical topology
- Method of transmitting on the media

2. **Logical Link Control**

- Connection Services: Flow Control and Error Control(mathematically calculates the checksum and compare it with received checksum)
- Synchronizing Transmission: Isochronous, Asynchronous (parity check) and Synchronous(Cyclic Redundancy Check)

### Layer 3 The Network Layer

- Logical Addressing: uses IP

- Switching: Packet Switching, Circuit Switching and Message Switching

- Route Discovery and Selection

- Connection Services: Flow Control and packet Reordering

  

### Layer 4 The Transport Layer

This layer acts as abridge between upper layer and lower layer. Message coming from the upper layer is encapsulated into segments for transport and data stream coming from lower layer is de-encapsulated and sent to layer 5.

- Transmission Control Protocol(TCP): connection oriented transport

- User Datagram protocol(UDP): connectionless transport
- Flow control in layer 4 are windowing and buffering
- Windowing: Receiver attest acknowledgement to the server informing all the segments are received, some time TCP can also use sliding window where the window increases exponentially
- `Round trip time` aka `Real Travel Time` is the length time it takes for a data packet to be sent to a  destination plus the time it takes for an acknowledgment of that packet  to be received back at the origin
- Buffering: When the bandwidth is not available, the router holds the segments in a buffer or queue, it has a finite capacity and sometime it can overflow in case of sustained network congestion

### Layer 5 The Session Layer

This layer can be treated as a conversation that needs to be treated separately from other session to prevent intermingling of the data.

It includes setting up session, maintaining session and tearing down a session.



### Layer 6 The Presentation Layer

This layer handles the formatting of data to be send and encryption of data.



### Layer 7 The Application Layer

This layer gives application service to the network. 

Two features of this layer are:

- Application Service
- Service Advertisement

## The TCP/IP Stack

Also Known as DoD model (United State Department of Defense)



![Model Compare](https://images2.imgbox.com/74/14/g7mqKStH_o.png)



Network Interface Aka Network Access Layer, includes Layer 1 and Layer 2 of OSI Model.



<u>Common Application Protocols in the TCP/IP Stack</u>

Ports numbered 1023 and below are called well-known ports, and ports num-
bered above 1023 are called ephemeral ports. The maximum value of a port is 65,535.
Well-known port number assignments are found at [here](http://www.iana.org/assignments/
port-numbers)



| Protocol  | Description                                                  | TCP port  | UDP port   |
| --------- | ------------------------------------------------------------ | --------- | ---------- |
| DHCP      | Dynamic Host Configuration Protocol: Dynamically assigns IP address information (for example, IP address, subnet mask, DNS server’s IP address, and default gateway’s IP address) to a network device |           | 67,68      |
| DNS       | Domain Name System: Resolves domain names to corresponding IP addresses | 53        | 53         |
| FTP       | File Transfer Protocol: Transfers files with a remote host (typically requires authentication of user credentials) | 20 & 21   |            |
| H.323     | A signaling protocol that provides multimedia communications over a network | 1720      |            |
| HTTP      | Hypertext Transfer Protocol: Retrieves content from a web server | 80        |            |
| HTTPS     | Hypertext Transfer Protocol Secure: Used to securely retrieve content from a web server | 443       |            |
| IMAP      | Internet Message Access Protocol: Retrieves email from an email server | 143       |            |
| IMAP4     | Internet Message Access Protocol Version 4: Retrieves email from an email server | 143       |            |
| LDAP      | Lightweight Directory Access Protocol: Provides directory services (for example, a user directory that includes username, password, email, and phone number information) to network clients | 389       |            |
| LDAPS     | Lightweight Directory Access Protocol over SSH: A secured version of LDAP | 636       |            |
| MGCP      | Media Gateway Control Protocol: Used as a call control and communication protocol for Voice over IP networks |           | 2427, 2727 |
| NetBIOS   | Network Basic Input/Output System: Provides network communication services for LANs that use NetBIOS | 139       | 137,138    |
| NNTP      | Network News Transport Protocol: Supports the posting and reading of articles on Usenet news servers | 119       |            |
| NTP       | Network Time Protocol: Used by a network device to synchronize its clock with a time server (NTP server) |           | 123        |
| POP3      | Post Office Protocol Version 3: Retrieves email from an email server | 110       |            |
| RDP       | Remote Desktop Protocol: A Microsoft protocol that allows a user to view and control the desktop of a remote computer | 3389      |            |
| rsh       | Remote Shell: Allows commands to be executed on a computer from a remote user | 514       |            |
| RTP       | Real-time Transport Protocol: Used for delivering media-based data (such as Voice over IP) through the network | 5004,5005 | 5004,5005  |
| RTSP      | Real-Time Streaming Protocol: Communicates with a media server (for example, a video server) and controls the playback of the server’s media files | 554       | 554        |
| SCP       | Secure Copy: Provides a secure file-transfer service over an SSH connection and offers a file’s original date and time information, which is not available with FTP | 22        |            |
| SFTP      | Secure FTP: Provides FTP file-transfer service over an SSH connection | 22        |            |
| SIP       | Session Initiation Protocol: Used to create and end sessions for one or more media connections, including Voice over IP calls | 5061      | 5060       |
| SMB       | Server Message Block: Used to share files, printers, and other network resources | 445       |            |
| SMTP      | Simple Mail Transfer Protocol: Used for sending email        | 25        |            |
| SNMP      | Simple Network Management Protocol: Used to monitor<br/>and manage network devices |           | 161        |
| SNMP Trap | Simple Network Management Protocol Trap: A notification sent from an SNMP agent to an SNMP manager | 162       | 162        |
| SNTP      | Simple Network Time Protocol: Supports time synchronization among network devices, similar to Network Time Protocol (NTP), although SNTP uses a less complex algorithm in its calculation and is slightly less accurate than NTP |           | 123        |
| SSH       | Secure Shell: Used to securely connect to a remote host (typically via a terminal emulator) | 22        |            |
| Telnet    | Telnet: Used to connect to a remote host (typically via a terminal emulator) | 23        |            |
| TFTP      | Trivial File Transfer Protocol: Transfers files with a remote host (does not require authentication of user credentials) |           | 69         |

