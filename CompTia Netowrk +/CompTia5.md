## Routing IP Packets

### Basic Routing Process

![step1](https://images2.imgbox.com/24/f3/qBsYq9M5_o.png)



![step2](https://images2.imgbox.com/68/a8/XYYMFYh2_o.png)



![](https://images2.imgbox.com/3e/ce/kkTP27Ze_o.png)



### “How does a router’s routing table become populated with entries?”

- Directly Connected Routes

- Static Routes
  - default static route
- Dynamic Routing Protocol
  - hop count
  - Open Shortest Path First (OSPF)
  - backup route convergence



**Routing Protocol Characteristics**



`routing protocol vs routed protocol`

A ``routed` protocol is a protocol by which data  can be routed. Examples of a routed protocol are IP, IPX, and AppleTalk. Required in such a protocol is an addressing scheme. Based on the  addressing scheme, you will be able to identify the network to which a  host belongs, in addition to identifying that host on that network. All  hosts on an internetwork (routers, servers, and workstations) can  utilize the services of a routed protocol.



A `routing` protocol, on the other hand, is only used between routers. Its purpose is to help routers building and maintain routing tables. A routing protocol (for example, RIP, OSPF, or EIGRP) is a protocol that advertises route information between routers.



**1. Believeability of Router**

The index of believability is called administrative distance (AD).

| Routing Information Source                          | Administrative Distance            |
| --------------------------------------------------- | ---------------------------------- |
| Directly Connected Network                          | 0                                  |
| Statically Connected Network                        | 1                                  |
| Enchanced Interior Gateway Routing Protocol (EIGRP) | 90                                 |
| Open Shortest Path First (OSPF)                     | 110                                |
| Routing Information Protocol (RIP)                  | 120                                |
| External EIGP                                       | 170                                |
| Unknown of unbelievable                             | 255 (Considered to be unreachable) |

2. **Metrices**

   A value assigned to a route. Lower metrices are preferred over higher metrices.

3.  **Interior vs Exterior Gateway Protocol**

   IGP operates within an autonomuos system where as EGP is used to provide routing information between different autonomous system.

4. **Route Advertisement Method**

   <u>Distance Vector</u>

   A distance-vector routing protocol sends a full copy of its routing table to its directly attached neighbors. This is a periodic advertisement.

   Since they advertise they routing information to eachother, there is a possibility of routing loop. And the metrics value keeps on increasing until it reaches an unreachable value (16 in case of RIP).

   Distance-vector routing protocols typically use one of two approaches for preventing routing loops:

   - Split horizon: The split-horizon feature prevents a route learned on one interface from being advertised back out of that same interface.
   - Poison reverse: the notifying gateway sets the number of hops to the unconnected gateway to a number that indicates *infinite* -- meaning, it is unreachable. Since RIP allows up to 15 hops to  another gateway, setting the hop count to 16 would mean infinite.

   <u>Link State</u>

   Rather than having neighboring routers exchange their full routing tables with one another, a link-state routing protocol allows routers to build a topological map of the network.

   Routers send link-state advertisements (LSAs) to advertise the networks they know how to reach. Routers then use those LSAs to construct the topological map of a network. The algorithm that runs against this topological map is Dijkstra’s shortest path first algorithm.

**Routing Protocol Examples**

- Routing Information Protocol (RIP): A distance-vector routing protocol that uses a metric of hop count. The maximum number of hops between two routers in an RIP-based network is 15. Therefore, a hop count of 16 is considered to be infinite. Also, RIP is an IGP.
- Open Shortest Path First (OSPF): A link-state routing protocol that uses a metric of cost, which is based on the link speed between two routers. OSPF is a popular IGP because of its scalability, fast convergence, and
  vendor-interoperability.
- Intermediate System-to-Intermediate System (IS-IS): This link-state routing protocol is similar in its operation to OSPF. It uses a configurable, yet dimensionless, metric associated with an interface and runs Dijkstra’s shortest path first algorithm.
- Enhanced Interior Gateway Routing Protocol (EIGRP): EIGRP is a Cisco proprietary protocol.Some literature calls EIGRP an advanced distance-vector routing protocol, and some literature calls it a hybrid routing protocol (mixing characteristics of both distance-vector and link-state routing protocols). EIGRP uses information from its neighbors to help it select an optimal route (like distance-vector routing protocols). However, EIGRP also maintains a database of topological information (like a link-state routing protocol). The algorithm EIGRP uses for its route selection is not Dijkstra’s shortest path first algorithm. Instead,
  EIGRP uses diffusing update algorithm (DUAL).
- Border Gateway Protocol (BGP): The only EGP in widespread use today. In fact, BGP is considered to be the routing protocol that runs the Internet.Although some literature classifies BGP as a distance-vector routing protocol, it can more accurately be described as a path-vector routing protocol, meaning that it can use as its metric the number of autonomous system hops that must be transited to reach a destination network, as opposed to a number of required router hops.

A network can simultaneously support more than one routing protocol through the
process of `route redistribution`.



### Network Address Translation

| NAT IP Address | Definition                                         |
| -------------- | -------------------------------------------------- |
| Inside Local   | A private IP address referencing an inside device  |
| Inside Global  | A public IP address referencing an inside device   |
| Outside Local  | A private IP address referencing an outside device |
| Outside Global | A public IP address referencing an outside device  |

DNAT: Dynamic NAT aka many-to-many

SNAT: Static NAT aka many-to-one

PAT: Port Address Translation aka many-to-one

### Multicast Routing

Two primary protocols used for multicast are Internet Group Management Protocol (IGMP) and Protocol Independent Multicast (PIM).

**IGMP:** 

- IGMPv1: IGMP report message sent by the PC that wants to join the multicast
- IGMPv2: supports a leave message
- IGMPv3: Adds feature called Source-specific multicast(SSM) which allows a client to request traffic not only destined for a particular multicast group but also sourced from a specific server

switch has IGMP snooping feature

**PIM:**

PIM’s main purpose is to form a multicast distribution tree, which is the path (or paths) over which multicast traffic flows.

- PIM-DM: PIM dense mode, uses source distribution tree, initially traffic from multicast source is flooded to all the networks, if the traffic is not needed by the router, it sends prune message to its neighbouring router, drawback is flood and prune behaviour

- PIM-SM: PIM spare mode, uses shared distribution tree, traffic from the source router is send to the rendezvous point (another router) and it receives IGMP join message from the last hop router from client. Then the last hop router will form the optimal route through a behaviour called shortest path tree(SPT) switchover.

   
