# OSPF Design

## 1. Project Overview

This project implements a multi-area Open Shortest Path First (OSPF) enterprise network using Cisco routers and switches in Cisco Packet Tracer.

The network demonstrates:

* OSPF Area 0 backbone design
* Multiple OSPF areas
* Area Border Routers (ABRs)
* OSPF router IDs
* OSPF neighbor adjacencies
* Inter-area route exchange
* Default-route propagation
* External ISP connectivity
* End-to-end connectivity testing

---

## 2. Network Architecture

The network consists of:

* R1 — Core Router
* R2 — Area Border Router (ABR)
* R3 — Area Border Router (ABR)
* R4 — Edge Router
* ISP — External Router
* SW1, SW2, SW3 — Access Switches
* PC1–PC6 — End-user devices

---

## 3. OSPF Area Design

### Area 0 — Backbone

Area 0 forms the OSPF backbone of the enterprise network.

R1 operates as the core router.

| Router | Interface | Network |
|---|---|---|
| R1 | G0/0 | 10.0.12.0/30 |
| R1 | G0/1 | 10.0.13.0/30 |
| R1 | G0/2 | 10.0.14.0/30 |
| R1 | Lo0 | 1.1.1.1/32 |
| R2 | G0/0 | 10.0.12.0/30 |
| R3 | G0/0 | 10.0.13.0/30 |
| R4 | G0/0 | 10.0.14.0/30 |
| R4 | Lo0 | 4.4.4.4/32 |

### Area 10

Area 10 represents the first internal LAN.

R2 acts as the Area Border Router between Area 0 and Area 10.

Area 10 contains:

* 192.168.10.0/24
* R2 Loopback0 — 2.2.2.2/32

R2 G0/1 provides the default gateway for the Area 10 LAN.

The Area 10 end devices are:

* PC1 — 192.168.10.10
* PC2 — 192.168.10.11

### Area 20

Area 20 represents the second internal LAN section.

R3 acts as the Area Border Router between Area 0 and Area 20.

Area 20 contains:

* 192.168.20.0/24
* 192.168.30.0/24
* R3 Loopback0 — 3.3.3.3/32

R3 provides the gateways for both Area 20 LANs.

The Area 20 end devices are:

* PC3 — 192.168.20.10
* PC4 — 192.168.20.11
* PC5 — 192.168.30.10
* PC6 — 192.168.30.11

---

## 4. Router Roles

| Router | Role | OSPF Areas |
|---|---|---|
| R1 | Core Router | Area 0 |
| R2 | Area Border Router | Area 0 / Area 10 |
| R3 | Area Border Router | Area 0 / Area 20 |
| R4 | Edge Router | Area 0 |
| ISP | External Router | External Network |

R2 and R3 are ABRs because each has one interface connected to Area 0 and additional interfaces participating in another OSPF area.

---

## 5. OSPF Router IDs

| Router | Router ID |
|---|---|
| R1 | 1.1.1.1 |
| R2 | 2.2.2.2 |
| R3 | 3.3.3.3 |
| R4 | 4.4.4.4 |

Loopback interfaces are used for stable router identification.

---

## 6. OSPF Adjacencies

R1 forms OSPF neighbor relationships with:

* R2 — FULL
* R3 — FULL
* R4 — FULL

These adjacencies provide the Area 0 backbone connectivity required for route exchange.

---

## 7. Inter-Area Routing

R2 advertises the Area 10 network:

`192.168.10.0/24`

into the Area 0 backbone.

R3 advertises the Area 20 networks:

`192.168.20.0/24`

and

`192.168.30.0/24`

into the Area 0 backbone.

The routing table on R1 therefore contains routes to all three internal LANs.

---

## 8. Default Route Propagation

R4 provides the connection between the enterprise OSPF network and the external ISP.

The external connection uses:

* R4 G0/1 — 203.0.113.1/24
* ISP G0/0 — 203.0.113.2/24

R4 has a static default route:

`0.0.0.0/0 → 203.0.113.2`

R4 advertises this default route into OSPF using:

`default-information originate`

Internal routers can therefore use R4 as the path toward external networks.

---

## 9. Connectivity Verification

The following tests were successfully completed:

### Internal Connectivity

* PC1 → PC3 — Successful
* PC1 → PC5 — Successful
* PC3 → PC1 — Successful
* PC5 → PC1 — Successful

### External Connectivity

* PC1 → ISP — Successful
* PC3 → ISP — Successful
* PC5 → ISP — Successful

These tests demonstrate successful routing between the different OSPF areas and toward the external network.

---

## 10. Key Networking Concepts Demonstrated

This project demonstrates practical knowledge of:

* Cisco IOS configuration
* IPv4 addressing
* Subnetting
* /30 point-to-point networks
* OSPF
* OSPF Area 0
* Multi-area OSPF
* Area Border Routers
* Router IDs
* OSPF neighbor relationships
* Route advertisement
* Inter-area routing
* Default-route propagation
* Static routing
* Enterprise network segmentation
* Network troubleshooting
* End-to-end connectivity testing
