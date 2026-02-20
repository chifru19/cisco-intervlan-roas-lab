# Inter-VLAN Routing: Router-on-a-Stick Implementation

## Project Overview
This repository contains a Cisco Packet Tracer laboratory demonstrating **Inter-VLAN Routing** using the "Router-on-a-Stick" (ROAS) methodology. The goal is to allow two isolated VLANs to communicate across a single physical router interface using 802.1Q trunking.

## Topology & Requirements
The network consists of a Cisco 2911 Router, a 2960 Switch, and two departmental PCs.

* **VLAN 10 (Sales):** 192.168.10.0/24
* **VLAN 20 (HR):** 192.168.20.0/24
* **Encapsulation:** IEEE 802.1Q
## 🛠️ Implementation Details

### 1. Layer 2 Segmentation (VLANs)
To reduce broadcast domains and improve security, I implemented **Virtual Local Area Networks (VLANs)**. 
- **VLAN 10 (Sales)** was assigned to port `Fa0/1`.
- **VLAN 20 (HR)** was assigned to port `Fa0/2`.
- Ports were moved from the default VLAN 1 to their respective departmental segments to ensure isolation.

### 2. IEEE 802.1Q Trunking
A **Trunk Link** was established on interface `Gig0/1` of the switch. Using the **802.1Q** protocol, this link allows the switch to send "tagged" frames from multiple VLANs over a single physical cable to the router.

### 3. Router-on-a-Stick (ROAS) Logic
I configured the **Cisco 2911 Router** with logical sub-interfaces to serve as the Default Gateway for each VLAN.
- **Sub-interface G0/0.10**: Handles traffic for 192.168.10.0/24.
- **Sub-interface G0/0.20**: Handles traffic for 192.168.20.0/24.
This allows inter-VLAN communication without requiring a separate physical router port for every network segment.

### 4. Connectivity Verification
Communication was confirmed through ICMP echo requests (pings). Successful replies were received between subnets, proving that the router is successfully de-encapsulating and re-routing traffic between the Sale and HR networks.


## Technical Configuration

### Router0 (Gateway)
The router uses sub-interfaces to provide a default gateway for each subnet.
* **Sub-interface G0/0.10:** Gateway for VLAN 10 (`192.168.10.1`).
* **Sub-interface G0/0.20:** Gateway for VLAN 20 (`192.168.20.1`).

### Switch0 (Infrastructure)
* **Trunk Port (G0/1):** Configured as a trunk to pass tagged traffic for VLANs 1, 10, and 20 to the router.
* **Access Ports:** Fa0/1 is assigned to VLAN 10; Fa0/2 is assigned to VLAN 20.
### Verification Evidence
Below are the confirmed ping results and interface statuses from the lab:

**Router Sub-interface Status (Up/Up):**
![Interface Status](Screenshot%202026-02-20%20at%2008.48.14.jpg)

**Successful Cross-VLAN Pings:**
![Ping Results](Screenshot%202026-02-19%20at%2022.20.16.jpg)
## Verification Results
Successful end-to-end connectivity was verified via ICMP:
1.  PC0 successfully pinged the local gateway (`192.168.10.1`).
2.  PC0 successfully pinged the remote gateway (`192.168.20.1`).
3.  Cross-VLAN communication between PC0 and PC2 was established.

## How to Use
1.  Download the `.pkt` file from the `Cisco_Packet_Tracer/` directory.
2.  Open in **Cisco Packet Tracer (v8.x recommended)**.
3.  Reference the `configs/` folder for the full Cisco IOS command history.
