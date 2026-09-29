# Enterprise OSPF Network Design and Implementation

## Overview

This project demonstrates the design, configuration, and verification of a multi-area OSPF enterprise network in Cisco Packet Tracer.

The topology includes multiple OSPF areas, Area Border Routers (ABRs), internal LANs, and connectivity to a simulated ISP.

## Network Components

- 4 Cisco 2911 routers
- 1 ISP router
- 3 Cisco 2960 switches
- 6 end-user PCs
- OSPF Areas 0, 10, and 20
- External ISP connectivity

## Topology

[View the Network Topology PDF](Documentation/Network-Topology.pdf)

```text
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

## OSPF Design

The network uses a hierarchical, multi-area OSPF architecture.

### Area 0 — Backbone

Area 0 provides the OSPF backbone and connects the core, ABRs, and edge router.

- R1: Core router
- R2: ABR for Area 10
- R3: ABR for Area 20
- R4: Edge router

### Area 10

Area 10 contains the LAN connected to R2.

- Network: `192.168.10.0/24`
- Gateway: `192.168.10.1`
- Router: R2

### Area 20

Area 20 contains the LANs connected to R3.

- Network: `192.168.20.0/24`
- Gateway: `192.168.20.1`
- Network: `192.168.30.0/24`
- Gateway: `192.168.30.1`
- Router: R3

## Router Roles

| Router | Role | OSPF Areas |
|---|---|---|
| R1 | Core router | Area 0 |
| R2 | Area Border Router | Areas 0 and 10 |
| R3 | Area Border Router | Areas 0 and 20 |
| R4 | Edge router | Area 0 |
| ISP | External router | Not running OSPF |

## Router IDs

| Router | Router ID |
|---|---|
| R1 | `1.1.1.1` |
| R2 | `2.2.2.2` |
| R3 | `3.3.3.3` |
| R4 | `4.4.4.4` |

## IP Addressing

The design uses:

- `/30` subnets for point-to-point router links
- `/24` subnets for enterprise LANs
- `/32` loopback addresses for router identification

For the complete addressing plan, see the [IP Addressing Table](Documentation/IP-Addressing-Table.md).

## External Connectivity

R4 connects the enterprise network to the simulated ISP.

A static default route points toward the ISP, and R4 advertises that route into OSPF with:

```text
default-information originate
```

The ISP includes return routes to the enterprise networks, enabling internal PCs to reach the simulated external network.

## Configuration Files

Complete router and switch configurations are available in the `Configurations` directory:

- [R1 Configuration](Configurations/R1-Configuration.txt)
- [R2 Configuration](Configurations/R2-Configuration.txt)
- [R3 Configuration](Configurations/R3-Configuration.txt)
- [R4 Configuration](Configurations/R4-Configuration.txt)
- [ISP Configuration](Configurations/ISP-Configuration.txt)
- [Switch Configurations](Configurations/Switch-Configurations.txt)

## Verification

OSPF operation was verified with the following Cisco IOS commands:

```text
show ip ospf neighbor
show ip ospf interface brief
show ip route
show ip protocols
```

The routers established full OSPF adjacencies. R1 formed FULL adjacencies with R2, R3, and R4.

Connectivity testing covered:

- Router-to-router communication
- LAN gateway reachability
- Inter-area PC connectivity
- Access to the simulated ISP

The tests confirmed:

- Inter-area routing
- LAN-to-LAN connectivity
- Default-route propagation
- External connectivity

Detailed results are available in the `Verification` directory.

## Troubleshooting

Implementation issues included:

- Interfaces assigned to incorrect OSPF areas
- Misinterpreted OSPF neighbor states
- Incorrect subnet masks
- Missing ISP return routes
- Routing-related connectivity failures

Resolving these issues validated the final network design and configuration.

## Project Structure

```text
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
```

## Technologies and Skills

- Cisco Packet Tracer
- Cisco IOS
- OSPF and multi-area OSPF
- Area Border Routers (ABRs)
- IPv4 addressing and subnetting
- Static routing
- Default-route propagation
- LAN/WAN networking
- Network troubleshooting
- Routing verification

## Objective

This project demonstrates practical skills in enterprise network design, OSPF configuration, IPv4 addressing, routing, troubleshooting, and network verification using Cisco technologies.
