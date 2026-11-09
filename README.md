
# TechCorp Enterprise Network — Multi-Site Infrastructure Design & Implementation

> A full enterprise network built from scratch in Cisco Packet Tracer, covering network design, Layer 2/3 implementation, redundancy, dynamic routing, security, and WAN connectivity across three sites.

---

## Project Overview

This project simulates the network infrastructure of a fictional mid-sized company called TechCorp, operating across a main headquarters and two branch offices. It was built as a hands-on portfolio project to demonstrate practical enterprise networking skills at a junior network engineer level.

The network was designed and implemented across six structured phases, each targeting a specific layer of the stack — from IP addressing and VLAN design all the way through to encrypted VPN tunnels and application-layer services.

---


## Technologies Implemented

| Technology | Details |
|---|---|
| **VLAN Segmentation** | 7 VLANs — Management, HR, IT, Finance, Sales, Data Center, DMZ |
| **VLSM IP Design** | Subnets sized per department host count — /26, /27, /28, /29, /30 |
| **802.1Q Trunking** | All switch-to-switch links, native VLAN hardened to VLAN 999 |
| **Inter-VLAN Routing** | Layer 3 SVIs on HQ-CORE-SW1 with ip routing |
| **HSRP** | Gateway redundancy on all 5 user VLANs — Active/Standby across dist switches |
| **STP** | Core Switch set as root bridge for all VLANs |
| **OSPFv2** | Area 0 across HQ-EDGE-R1, Core Switch, Dist Switches, and both branch routers |
| **NAT/PAT** | Overload NAT for internet access + Static NAT for DMZ web server |
| **Extended ACLs** | Department isolation (Finance ↔ HR blocked) + DMZ isolation + inbound internet filtering |
| **Site-to-Site VPN** | IPSec IKEv1, AES encryption, SHA hashing, pre-shared key — HQ to Branch 1 |
| **DHCP** | Pools for all 6 user subnets on Core Switch with ip helper-address relay |
| **DNS** | Internal name resolution for techcorp.com hosted on Data Center server |
| **DMZ** | Public web server isolated from internal network via VLAN + ACL |

---

## IP Addressing Summary

### HQ VLANs

| VLAN | Name | Subnet | Mask | Gateway |
|---|---|---|---|---|
| 10 | Management | 192.168.10.0 | /28 | 192.168.10.1 |
| 20 | HR | 192.168.20.0 | /26 | 192.168.20.1 |
| 30 | IT | 192.168.30.0 | /27 | 192.168.30.1 |
| 40 | Finance | 192.168.40.0 | /27 | 192.168.40.1 |
| 50 | Sales | 192.168.50.0 | /26 | 192.168.50.1 |
| 100 | Data Center | 10.0.100.0 | /29 | 10.0.100.1 |
| 200 | DMZ | 10.0.200.0 | /29 | 10.0.200.1 |

### WAN Links

| Link | Subnet | HQ IP | Branch IP |
|---|---|---|---|
| HQ ↔ ISP | 203.0.113.0/30 | 203.0.113.2 | 203.0.113.1 |
| HQ ↔ Branch 1 | 10.10.10.0/30 | 10.10.10.1 | 10.10.10.2 |
| HQ ↔ Branch 2 | 10.10.20.0/30 | 10.10.20.1 | 10.10.20.2 |
| Branch 1 LAN | 172.16.1.0/25 | 172.16.1.1 | — |
| Branch 2 LAN | 172.16.2.0/26 | 172.16.2.1 | — |

---

## Project Phases

| Phase | Focus | Key Technologies |
|---|---|---|
| 1 | Network Design & IP Planning | VLSM, topology design, device inventory |
| 2 | VLANs, Trunking & Inter-VLAN Routing | 802.1Q, SVIs, ip routing, STP |
| 3 | Redundancy | HSRP, preempt, Active/Standby election |
| 4 | WAN Routing | OSPFv2, router-id, default-information originate |
| 5 | Security | Extended ACLs, NAT/PAT, Static NAT, DMZ |
| 6 | Services | DHCP, DNS, Site-to-Site IPSec VPN |

---

## Key Troubleshooting Scenarios

Real issues encountered and resolved during implementation:

- **Native VLAN mismatch** — CDP-4 warning triggered after hardening trunk links; resolved by applying VLAN 999 consistently on both ends of every trunk
- **STP port blocking** — STP blocked a dist switch port due to VLAN inconsistency; resolved automatically after native VLAN fix
- **HSRP stuck in Init** — Distribution switches had no trunk link between them; HSRP hellos could not flow; resolved by adding inter-dist trunk
- **OSPF adjacency failure** — Core Switch Gig0/1 had IP processing disabled (still a switchport); resolved with `default interface` + `no switchport`
- **NAT not translating** — NAT_SOURCES ACL was missing; created standard ACL with all internal subnets
- **Internet unreachable from PCs** — Distribution switches not running OSPF; no default route learned; added OSPF on both dist switches
- **ICMP blocked by inbound ACL** — INTERNET_INBOUND ACL missing `permit icmp` rule; added at top of ACL

---

## Files in This Repository

| File | Description |
|---|---|
| `TechCorp_Enterprise.pkt` | Cisco Packet Tracer project file |
| `TechCorp_Enterprise_Network.docx` | Full technical design document |
| `README.md` | This file |

---

## Tools Used

- **Cisco Packet Tracer** — Network simulation
- **Cisco IOS** — All device configuration
- **Cisco 2911, 3560, 2960** — Router and switch models used

---

## About

Built by Jwamer — Information System Engineering student, Erbil Polytechnic University.
=======
# TechCorp_Enterprise_Network
>>>>>>> d547662167ce61c22673d0ba5dfc177c722d9be5
