# GW
default gateway

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
