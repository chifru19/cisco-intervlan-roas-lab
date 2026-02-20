# Inter-VLAN Routing: Router-on-a-Stick Implementation

## Project Overview
This repository contains a Cisco Packet Tracer laboratory demonstrating **Inter-VLAN Routing** using the "Router-on-a-Stick" (ROAS) methodology. The goal is to allow two isolated VLANs to communicate across a single physical router interface using 802.1Q trunking.

## Topology & Requirements
The network consists of a Cisco 2911 Router, a 2960 Switch, and two departmental PCs.

* **VLAN 10 (Sales):** 192.168.10.0/24
* **VLAN 20 (HR):** 192.168.20.0/24
* **Encapsulation:** IEEE 802.1Q



## Technical Configuration

### Router0 (Gateway)
The router uses sub-interfaces to provide a default gateway for each subnet.
* **Sub-interface G0/0.10:** Gateway for VLAN 10 (`192.168.10.1`).
* **Sub-interface G0/0.20:** Gateway for VLAN 20 (`192.168.20.1`).

### Switch0 (Infrastructure)
* **Trunk Port (G0/1):** Configured as a trunk to pass tagged traffic for VLANs 1, 10, and 20 to the router.
* **Access Ports:** Fa0/1 is assigned to VLAN 10; Fa0/2 is assigned to VLAN 20.

## Verification Results
Successful end-to-end connectivity was verified via ICMP:
1.  PC0 successfully pinged the local gateway (`192.168.10.1`).
2.  PC0 successfully pinged the remote gateway (`192.168.20.1`).
3.  Cross-VLAN communication between PC0 and PC2 was established.

## How to Use
1.  Download the `.pkt` file from the `Cisco_Packet_Tracer/` directory.
2.  Open in **Cisco Packet Tracer (v8.x recommended)**.
3.  Reference the `configs/` folder for the full Cisco IOS command history.
