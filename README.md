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



(to be continued...)
