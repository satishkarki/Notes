## Network Components

### Media

`10BASE2`: The name *10BASE2* is derived from several characteristics of the physical medium. The *10* comes from the transmission speed of 10 [Mbit/s](https://en.wikipedia.org/wiki/Megabit_per_second).  The *BASE* stands for [baseband](https://en.wikipedia.org/wiki/Baseband) signalling, and the *2* for a maximum segment length approaching 200 m (the actual maximum length is 185 m).

**Coaxial Cable**

- Resistance to EMI/RFI
- Common types of coax cable:RG-58, RG-59, and RG-6
- RG prefix stands for Radio Guide
- Connectors: BNC(Bayonet Neill- Concelmn aka British Naval Connector) and F-connector(aka F-type)

**Twisted Pair Cable**

- Today's most popular LAN media type
- Two Types: Sheilded Twisted Pair(STP) and Unshielded Twisted Pair(UTP)
- STP: metallic sheilding on each twsited pair
- UTO: no metallic shielding but more twist per cm, less expensive and most commonly used
- Common category of UTP
  - Category 3: aka CAT3, used in 10BASE-T, carries data at a rate of 10Mbit/s
  - Category 5: used in 10BASE-TX, carries data at a rate of 100Mbit/s
  - Category 5e: used in 10BASE-T, carries data at a rate of 1Gbit/s
  - Category 6: used in 10BASE-T, similar to CAT5e
  - Category 6e: used in 10GBASE-T, 10Gbit/s

- RJ-45 connection is `straight-through` but for the purpose of connection lets say between two PC `crossover` connection is done
- Common Connectors: RJ-45(Registered Jack), RJ-11, DB-9(RS-232)
- Plenum vs Nonplenum cable

**Fibre-Optic Cable**

- Multi Mode Fibre(MMF) and Single Mode Fibre(SMF)
- Inner layer is called core and outer layer is called cladding, both have different refractive index so light bounces back inside and cannot escape
- Light bounced at different angle can have difference in time to travel such situation is called `multi mode distortion` so MMF is for short distance
- Connectors: ST(Straight Tip), SC(subscriber connector, standard conncetor,square connector), LC(Lucent Connector), MT-RJ(Media Termination Recomended Jack)
- Fibre Connection Polishing Style: Physical Contact(PC), Ultra Physical Contact(UPC), Angled Physical Contact(APC)

**Cable Distribution**

- Carrie =>Main Distribution Frame => Intermediate Distribution Frame => End user
- Two most popular IDF: 66 block and 110 block

 **Wireless Technologies**

Z-Wave, Ant+, Bluetooth, Near Field Connection(NFC), IR, RFID, 802.11



### Network Infrastructure Devices

**Hub**

- aka bit spitter
- Types: Active hub, Passive hub and Smart hub
- One collison domain and one broad cast domain

**Bridges**

- Two collison domain and one broadcast domain
- Bridge is a layer 2 device

**Switches**

- Multiple collison domain and one broadcast domain
- A computer if wants to connect to a server, through the switch then it will send a ARP request(lets assume IP is resoled by DNS), the switch will then store the MAC address of the source and forward the ARP request to all other ports. It does so because the ARP request has a destination MAC address of FFFF.FFFF.FFFF which  is not stored by the switch and it forwards to every other available port and when it reaches to the server it stores the MAC address of computer sending the ARP request and send back the ARP received response, now the switch will store the MAC address of the server and forward the ARP response back to the sending computer. Here we can consider switch to be working at layer 2.

**Multilayer Switchs**

Many literature consider it as a level 3 switch because of the capability to forward traffic based upon the IP protocol acting as a router.



**Router**

Similar to the multilayer switch but rich in other interface feature



**Infrastructure Device Summary**	

| Device             | Number of Collision Domain Possible | Number of Broadcast Domain Possible | OSI Layer Operation |
| ------------------ | ----------------------------------- | ----------------------------------- | ------------------- |
| Hub                | 1                                   | 1                                   | 1                   |
| Bridge             | 1 per port                          | 1                                   | 2                   |
| Switch             | 1 per port                          | 1 per port                          | 2                   |
| Multi Layer Switch | 1 per port                          | 1 per port                          | 3+                  |
| Router             | 1 per port                          | 1 per port                          | 3+                  |

### Specialized Network Devices

**VPN Concentrators**: Lets say the headqauter needs to connect to different remote sites, it can be done with a  secure tunnel on the internet known as the VPN(virtual private network). The process of encryption and authorization is involved which can be a heavy process to handle so VPN concentrators can be used at the end point of each site to do the heavy processing. It falls into the `encryption device` category.



**FireWall**: A `statefull` firewall allows traffic originated internally to travel to the internet and allows the response from the internet but blocks the request originated from the internet



**DNS servers**: It maintians the database of Fully Qualified Domain Name (FQDN) which gets converted to the IP address. 

FQDN Structure: **[hostname].[domain].[tld].**

For example, "www.satishkarki.com." is an FQDN since it contains a  hostname ("www") and a domain name ("satishkarki.com"), followed by a  trailing period. The name "satishkarki.com" is not fully qualified because it does not include a hostname or end with a period.

An FQDN can be broken down into four parts:

- [Hostname](https://techterms.com/definition/hostname): www, mail, ftp, store, support, etc.
- [Domain](https://techterms.com/definition/domain): apple, microsoft, ibm, facebook, etc.
- [Top level domain](https://techterms.com/definition/domain_suffix) (TLD): .com, .net, .org, .co.uk, etc.
- Trailing period: the final period in an FQDN indicates the end of the name, implying the previous string is the TLD.

Learn more about FQDN [here](https://techterms.com/definition/fqdn)

DNS Record: [DNS](https://techterms.com/definition/dns) records are stored in [zone files](https://techterms.com/definition/zonefile) and are used for translating [domain names](https://techterms.com/definition/domain_name) to [IP addresses](https://techterms.com/definition/ip_address).

```bash
;   Nameservers
;
     IN   NS   ns1.4servers.com.   ; 123.456.789.01
     IN   NS   ns2.4servers.com.   ; 123.456.789.02
;
;   Domain Mail Handlers
;
yourdomain.com.     IN   MX   0   mail
yourdomain.com.     IN   MX  10   mail
;
;
;   hosts in order
;
yourdomain.    IN   A   Your.IP.XXX
www            IN   A   Your.IP.XXX
smtp           IN   CNAME   www
pop            IN   CNAME   www
ftp            IN   CNAME   www
mail           IN   A   Your.IP.XXX
;
; end
```

 

| Record Type | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| A           | An address record (that is, A record) maps a hostname to an IPv4 address. |
| AAAA        | An IPv6 address record (that is, AAAA record) maps a hostname to an IPv6 address. |
| CNAME       | A canonical name record (that is, CNAME record) is an alias of an existing record, thus allowing multiple DNS records to map to the same IP address. |
| MX          | A mail exchange record (that is, MX record) maps a domain name to an email (or message transfer agent) server for that domain. |
| NS          | Delegates a DNS zone to use the given authoritative name servers. |
| PTR         | A pointer record (that is, PTR record) points to a canonical name. A PTR record is commonly used when performing a reverse DNS lookup, which is a process used to determine what domain name is associated with a known IP address. |
| SOA         | A start of authority record (that is, SOA record) provides authoritative information about a DNS zone, such as email contact information for the zone’s administrator, the zone’s primary name server, and various refresh timers. |
| SRV         | A generalized service location record. Used for newer protocols instead of creating protocol-specific records such as MX. |
| TXT         | Originally for arbitrary human-readable text in a DNS record. Since the early 1990s, however, this record carries machine-readable data, such as specified by RFC 1464, opportunistic encryption, Sender Policy Framework (SPF), or DomainKeys Identified Email (DKIM). |

URL(Uniform Resource Locater): https://www.satishkarki.com i.e https://FQDN



**DHCP Server**

Dynamic Host Configuration Protocol, 

`DORA`: Discover, Offer, Request, Acknowledgment

Client sents a broadcast message of DHCPDISCOVER with destination IP of 255.255.255.255 which is picked up by the DHCP Server. If there are multiple servers then the client will receive the DHCPOFFER sent to it first. DHCPOFFER will be unicast. Then the client will send the DHCPREQUEST unicast asking to provide the IP configuration parameters. The server will response with DHCPACK unicast.

Other terminologies: IP Helper, scope, lease, DHCP reservation



**Proxy Server**

A client requset the information in internet through the proxy server. 

A reverse proxy accepts the requst from clients on behalf of the server.

Benefits: Security, Content caching, content filtering



**Content Engine**: dedicated to content caching

**Content Switching**: also known as load balancing

**Wireless Range Extender, Next Generation FireWall, Software Defined Networking(SDN) controller**



## Voice Over Internet Protocols and Components



![VOIP](https://images2.imgbox.com/bb/80/cMZaq2Mj_o.png)

| Protocol/Device | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| IP Phone        | An IP phone is a telephone with an integrated Ethernet connection. Although users speak into a traditional analog handset (or headset) on the IP phone, the IP phone digitizes the spoken voice, packetizes it, and sends it out over a data network (via the IP phone’s Ethernet port). |
| Call Agent      | A call agent is a repository for a VoIP network’s dial plan. For example, when a user dials a number from an IP phone, the call agent analyzes the dialed digits and determines how to route the call toward the destination. |
| Gateway         | A gateway in a VoIP network acts as a translator between two different telephony signaling environments. In above figure, both gateways interconnect a VoIP network with the PSTN(Public Switched Telephone Network). Also, the gateway on the right interconnects a traditional PBX with a VoIP network. |
| PBX             | A Private Branch Exchange (PBX) is a privately owned telephone switch traditionally used in corporate telephony systems. Although a PBX is not typically considered a VoIP device, it connects into a VoIP network through a gateway, as shown above. |
| Analog Phone    | An analog phone is a traditional telephone, like you might have in your home. Even though an analog phone is not typically considered a VoIP device, it can connect into a VoIP network via a VoIP adapter or, as shown above, via a PBX, which is connected to a VoIP network. |
| SIP             | Session Initiation Protocol (SIP) is a signaling, setup, and management protocol used with voice and video sessions over IP networks. SIP, in conjunction with other protocols, also specifies the encoder/decoder (codec) that will be used for voice and video connections over the network. |
| RTP             | Real-time Transport Protocol (RTP) is a protocol that carries voice (and interactive video). Notice in  the figure that the bidirectional RTP stream does not flow through the call agent. |
