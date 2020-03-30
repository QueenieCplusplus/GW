# GW
default gateway GW == default router of hosts.

Below Graphic shows that a AS (Atonomous System) has multiple connections to the Internet.


                                        to the internet
                                       /
                                      /
                                     /
                                   IR1      

                                                R3
                         R1            


                                     AS

    to the internet --- IR2
                                                 IR3
                                                  \
                                                   \
                                    R2              \ 
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

(to be continued...)
