Enterprise OSPF Network Design & Implementation

Overview

This project demonstrates the design, configuration, implementation, and verification of a multi-area OSPF enterprise network using Cisco Packet Tracer.

The network simulates an enterprise environment with multiple routing areas, Area Border Routers (ABRs), internal LANs, and external ISP connectivity.

Network Architecture

The network consists of:

* 4 Cisco 2911 enterprise routers
* 1 ISP router
* 3 Cisco 2960 switches
* 6 end-user PCs
* OSPF Areas 0, 10, and 20
* External ISP connectivity

Topology

View Network Topology PDF

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

OSPF Design

The network uses a hierarchical multi-area OSPF design.

Area 0 — Backbone

Area 0 forms the OSPF backbone and connects the core and edge routers.

* R1 — Core router
* R4 — Edge router
* R2 — ABR
* R3 — ABR

Area 10

Area 10 serves the LAN connected to R2.

* Network: 192.168.10.0/24
* Gateway: 192.168.10.1
* Router: R2

Area 20

Area 20 serves the LANs connected to R3.

* Network: 192.168.20.0/24
* Gateway: 192.168.20.1
* Network: 192.168.30.0/24
* Gateway: 192.168.30.1
* Router: R3

Router Roles

Router	Role	OSPF Areas
R1	Core router	Area 0
R2	Area Border Router	Area 0 / Area 10
R3	Area Border Router	Area 0 / Area 20
R4	Edge router	Area 0
ISP	External router	Not running OSPF

Router IDs

Router	Router ID
R1	1.1.1.1
R2	2.2.2.2
R3	3.3.3.3
R4	4.4.4.4

IP Addressing

The network uses:

* /30 subnets for point-to-point router links
* /24 subnets for enterprise LANs
* /32 loopback addresses for router identification

Detailed addressing information is available in:

View IP Addressing Table

External Connectivity

R4 provides connectivity between the internal enterprise network and the external ISP.

R4 uses a static default route toward the ISP and advertises the default route into OSPF using:

default-information originate

The ISP has a return route toward the enterprise networks.

This allows internal PCs to reach the simulated external network.

Configuration

Complete router and switch configurations are available in the Configurations directory.

* R1 Configuration
* R2 Configuration
* R3 Configuration
* R4 Configuration
* ISP Configuration
* Switch Configurations

OSPF Verification

OSPF operation was verified using Cisco IOS commands including:

show ip ospf neighbor
show ip ospf interface brief
show ip route
show ip protocols

The routers successfully established OSPF neighbor relationships.

R1 established FULL OSPF adjacencies with:

* R2
* R3
* R4

Connectivity Testing

Connectivity was tested between:

* Enterprise routers
* Local LAN gateways
* PCs in different OSPF areas
* Internal networks and the simulated ISP

Successful tests demonstrated:

* Inter-area routing
* LAN-to-LAN connectivity
* Default-route propagation
* External connectivity

Detailed verification results are available in the Verification directory.

Troubleshooting

During implementation, several issues were identified and resolved, including:

* OSPF interfaces missing from the correct area
* OSPF neighbor-state interpretation
* Incorrect subnet masks
* External ISP return-route configuration
* Connectivity failures caused by routing configuration

The troubleshooting process helped validate the final network design.

Project Structure

enterprise-ospf-network-design/
│
├── README.md
│
├── Packet-Tracer/
│   └── Enterprise-OSPF-Network.pkt
│
├── Documentation/
│   ├── Network-Topology.pdf
│   ├── IP-Addressing-Table.md
│   └── OSPF-Design.md
│
├── Configurations/
│   ├── R1-Configuration.txt
│   ├── R2-Configuration.txt
│   ├── R3-Configuration.txt
│   ├── R4-Configuration.txt
│   ├── ISP-Configuration.txt
│   └── Switch-Configurations.txt
│
└── Verification/
    ├── OSPF-Neighbours.txt
    ├── OSPF-Routes.txt
    └── Connectivity-Tests.txt

Technologies and Skills

* Cisco Packet Tracer
* Cisco IOS
* OSPF
* Multi-area OSPF
* Area Border Routers (ABRs)
* IPv4 addressing
* Subnetting
* Static routing
* Default-route propagation
* LAN/WAN networking
* Network troubleshooting
* Routing verification

Objective

The objective of this project was to demonstrate practical knowledge of enterprise network design, OSPF configuration, routing, troubleshooting, and network verification using Cisco technologies.
