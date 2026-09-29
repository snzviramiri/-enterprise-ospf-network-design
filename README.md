# Enterprise OSPF Network Design & Implementation

## Project Overview

This project demonstrates the design, configuration, and verification of a multi-area enterprise network using Cisco routers, switches, and OSPF.

The network was built and tested in Cisco Packet Tracer to demonstrate practical skills in:

- Enterprise network design
- IPv4 addressing and subnetting
- OSPF configuration
- OSPF multi-area architecture
- Area Border Routers (ABRs)
- Inter-area routing
- Default-route propagation
- LAN connectivity
- Router-to-router connectivity
- External/ISP connectivity
- Network troubleshooting and verification

---

## Network Architecture

The network consists of:

- 4 Cisco 2911 enterprise routers
- 1 ISP router
- 3 Cisco 2960 switches
- 6 end-user PCs
- OSPF Areas 0, 10 and 20
- An external ISP connection

### Topology

[View Network Topology PDF](Documentation/Network Topology.pdf)

                         ISP
                          |
                         R4
                          |
                         R1
                       /    \
                     R2      R3
                     |      /  \
                    SW1    SW2  SW3
                   /  \    / \  / \
                 PC1 PC2 PC3 PC4 PC5 PC6
```
