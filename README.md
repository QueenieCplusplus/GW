# GW
default gateway GW == default router of hosts.

Below Graphic shows that a AS (Atonomous System) has multiple connections to the Internet.


                                        to the internet
                                       /
                                      /
                                     /
                             _____ IR1______     
                            /               \
                          /                  \    
                         R1                   R3
                         |                     |
                         |                     |
                         |          AS         |
                         |                     |
    to the internet --- IR2                    |
                          \                   IR3
                           \                  /    \
                            \_____     ______/      \
                                    R2               \ 
                                                      to the internet


Cisco's Routing Algortithm (nomatter the classful or classless) is extended by the concept of the GW of last resort.

The GW of last resort is a router that receive the traffic whose destination has no match in the routing table. This is similar to default GW or default router of hosts.

# GW of Host & Router

Hosts have small routing tables typically, thus use the deafault GW intensively (hosts have no many choices). On contrast, routers have big routing table, thus shall only use the GW of last resort. (Routers have several next-hop routers, and shall choose one that is the closest to traffic destination.)

# Router in connection to the Internet

The number of routes in Internet is huge, and making the routers of all network conected to the Internet to learn, it shall create excessive loads on these routers.

This loading can be avoided by utilizing the GW of last resort on these Routers, thus if the destination of some traffic is not found inside the network, it still can be accessible thru Internet.

# Candidate Default Routes

before a router choose the GW if the last resort, it shall have the candidate default routes.

below 3 create way explains how candidate default routers get to a router's routing table.

(1)All routes for network prefix 0.0.0.0/0 become the candidate default route.

       pseudo-connected routes == static routes pointing to an interface
       
       routes created by dynamic routing protocol, such as RIP or OSPF

(2) By entering one or several ip addr as below cmd, all routes whose network prefixes == ip addr, param of command, thus become candidate default routes.

       ip default-network <IP addr>

(3) In IGRP, advertising network prefixes as exterior, thus the routes become candidate default routes.

# to choose the best in the Candidate Default Routes

1. If any candidate default connected routes is present, then exclude them from the list.

2. If several candidate default routes exist, only the one with the smallest admin distance are kept, if there is only one, then it means this is the one that chosen by algorithm.

3. step1 , the one chosen by the smallest metric.

4. step2, there are several result, then choose the one that created first.

# to create the GW of last resort

If the router decides to create the GW of the last resort, it makes itself equal to the IP addr of the next-hop router of the chosen candidate default route.

a. Connected Created Routes, the router creates the GW of the last resort.

b. Statice Created Routes, the algorithm creates the GW of the last resort.

c. Dynamic Created Routes, the algorithm does not create GW of the last resort.

# Routing Table of Router

    R0$ show ip route


    Codes: R - RIP
           O - OSPF
           S - Stactic
           U - Per User Static Route
           B - BGP
           i - IS-IS
           * - Candidate Default
           D - EIGRP
           I - IGRP
       
    Gateway at last resort is 10.0.1.1 to network 192.168.31.o0
       
      I 192.168.31.0/24 [100/10576] via 10.0.1.1 00:00:05. Serial0
      |          |       | |           |                      |
      V          |       | |           V                      |
      source of routing info           Next Hop Router        V
                 |       | |                                  Output of interface
                 V       | V
                 Mask    V metrics
                         Distance of Route
                         
                         ... (others)
                         
      C 192.168.100.0/24 is directly connected. Ethernet0
         
if below cmd executes
  
      R0$ ip default-network 192.168.100.0
      > this cmd makes the connected route thru interface E0 a candidate default route.
      
the routing table then changed as following
                  
      R0$ show ip route


      Codes: R - RIP
             O - OSPF
             S - Stactic
             U - Per User Static Route
             B - BGP
             i - IS-IS
             * - Candidate Default
             D - EIGRP
             I - IGRP
       
      Gateway of last resort is not set
      
      I 192.168.31.0/24 [100/10576] via 10.0.1.1 00:00:05. Serial0
                         
                         ... (others)
                         
      C 192.168.100.0/24 is directly connected. Ethernet0
     

(to be continued...)
