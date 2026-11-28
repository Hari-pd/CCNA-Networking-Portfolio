# Entreprise Network: Hands-on Lab.


## 1. Project Overview

This is a hands-on networking project for a company with two offices, HQ and a branch office. The project involves my learning from the CCNA course and the goal is to apply the networking concepts I have studied in a practical environment using Cisco Packet Tracer. The project will cover the learnings of VLANs, inter-VLAN routing, STP concepts, EtherChannel, DHCPv4, DHCPv6, SLAAC and FHRP concepts.



## 2. Project Objectives


A. Design a scalable dual-stack network connecting HQ and branch office.

B. Configure IPv4 an dIPv6 addressing, DHCP services and default gateways.

C. Segment departments using VLANs to improve traffic separation.

D. Configure Layer 2 Switching, trunk links, inter-VLAN routing, and Layer 3 switching.

E. Implement network redundancy using STP, EtherChannel and FHRP.





## 3. Network Requirements


The network is designed around the following business and technical requirements:



**Location and Departments**



* HQ- Approximately 60 employees across Administration, HR, IT, Sales, and Customer support and Security departments.



* Branch- Approximately 30 employees, primarily supporting Customer support and Regional Operations.





**Network Segmentation**



* Separate departments into individual VLANs where appropriate.
* Provide suitable network connectivity between departments through Layer 3 routing.
* Support voice devices, printers, servers, and wireless clients.
* Provide a separate guest wireless network.





**Network Services**



* DHCP- A dedicated DHCP server provide automatic IPv4 address allocation at HQ. Layer 3 switch acts as a relay agent for IP allocation. In branch office, DHCP services are configured directly on Layer 3 switch using DHCP server functionality.
* Centralised servers- The main network services are hosted at HQ offices including DNS server. The branch office will access the centrally hosted services.





**Availability and Redundancy**







## 4. Network Devices and IP Address

| Device | Name | IP Address | Purpose |
| --- | --- | --- | --- |
| Layer-2 Switch | HQ-F1-SW-A | 10.10.99.1/24 | Access port and Trunk port targeted for VLAN 10 and 20 in First floor of the office. |
| Layer-2 Switch | HQ-F2_SW-B | 10.10.99.2/24 | Access port and Trunk port targeted for VLAN 30,40,50 and 60 in second floor of the office |


**Layer-3 Switch: Interfaces and IP Addresses**

For redundancy, two layer-3 switches were used. STP and HSRP configured to prevent switching loops and redundancy.

Layer-3 switch 1 name: HQ-SW1
Layer-3 switch 2 name: HQ-SW2

| interface | HQ-SW1 IP | HQ-SW2 IP | HSRP Virtual IP (default gateway for each VLANs) | Active Switch | Standby Switch |
| --- | --- | --- | --- | --- | --- |
| VLAN 10 | 10.10.0.1/26 | 10.10.0.2/26 | 10.10.0.3/26 | HQ-SW1 | HQ-SW2 |
| VLAN 20 | 10.10.0.65/26 | 10.10.0.66/26 | 10.10.0.67/26 | HQ-SW1 | HQ-SW2 |
| VLAN 30 | 10.10.1.1/26 | 10.10.1.2/26 | 10.10.1.3/26 | HQ-SW2 |  HQ-SW1 |
| VLAN 40 | 10.10.1.65/26 | 10.10.1.66/26 | 10.10.1.67/26 | HQ-SW2 | HQ-SW1 |
| VLAN 50 | 10.10.1.129/26 | 10.10.1.130/26 | 10.10.1.131/26 | HQ-SW2 | HQ-SW1 |
| VLAN 60 | 10.10.60.1 /24 | 10.10.60.2/24 | 10.10.60.3/24 | HQ-SW2 | HQ-SW1 |
| VLAN 99 | 10.10.99.254/24 | 10.10.99.4/24 | 10.10.99.5/24 | HQ-SW1 | HQ-SW2 |
| VLAN 101 | 10.10.10.1/26 | 10.10.10.4/26 | 10.10.10.5/26 | HQ-SW2 | HQ-SW1 |


## 5. IP address allocation

**IPv4 allocation**

| VLAN | Name | Network | Default Gateway | DHCP allocaton |
| --- | --- | --- | --- | --- |
| 10 | Admin | 10.10.0.0/26 | 10.10.0.3 | 10.10.0.5 - 10.10.0.24 (20 devices) |
| 20 | HR | 10.10.0.64/26 | 10.10.0.67 | 10.10.0.70 - 10.10.0.89 (20 devices) |
| 30 | IT | 10.10.1.0/26 | 10.10.1.3 | 10.10.1.5 - 10.10.1.24 (20 devices) |
| 40 | Sales | 10.10.1.64/26 | 10.10.1.67 | 10.10.1.70 - 10.10.1.89 (20 devices) |
| 50 | CS-and-Sec | 10.10.1.128/26 | 10.10.1.131 | 10.10.1.135 - 10.10.1.154 (20 devices) |
| 60 | GUEST-CONNECT | 10.10.60.0/24 | 10.10.60.3 | 10.10.60.100 - 10.10.60.149 (50 devices) |
| 99 | Mgmt | 10.10.99.0/24 | 10.10.99.5 | manually assigned IP to devices |
| 101 | SRV | 10.10.10.0/26 | 10.10.10.5 | manually assigned IP to servers |


## 6. Configurations

**HQ-SW1**
 * Layer-3 routing between VLANS
 * HSRP gateway redundancy
 * STP Root bridge for selected VLANs
 * Trunk connection to other switches

! Enable Layer 3 routing
 ip routing

! Configure VLAN 99 management interface
| 'command' | what it does |
| --- | --- |
| 'interface vlan 99' | creates or enters the vlan interface |
| 'ip address 10.10.99.254 255.255.255.0' | allocate static ip to the interface |
| 'no shutdown' | enables the vlan |
| 'interface vlan 10' | creates or enters the vlan interface |
| 'ip address 10.10.0.1 255.255.255.192' | allocate static ip to the interface |
| 'no shutdown' | enables the interface |

! Configure Trunk port
| 'command' | what it does |
| --- | --- |
| 'interface f0/11' | enters interface configuration mode |
| 'switchport trunk encapsulation dot1q' | configure 802.1Q encapsulation |
| 'switchport mode trunk' | configure the interface to trunk port |
| 'switchport trunk native vlan 100' | configure vlan 100 as native vlan for the trunk port |
| 'switchport trunk allowed vlan 10,20,99,100' | configures to allow only vlan 10,20,99 and 100 to pass through the trunk port |

! Configure STP Root bridge
| 'command' | what it does |
| --- | --- |
| 'config t' | enters global configuration mode |
| 'spanning-tree vlan 10,20,99 root primary' | instructs the switch to become STP root bridge for vlan 10,20 and 99. |
| 'spanning-tree vlan 30,40,50,60,90,101,100 root secondary' | instructs the switch to become STP backup root bridge for selected vlans. If the root bridge of the selected vlans fail, this switch will be the root bridge. |

! Configure HSRP
| 'command' | what it does |
| --- | --- |
| 'interface vlan 99' | enters vlan configuration |
| 'standby 99 ip 10.10.99.5' | Add HSRP Virtual IP |
| 'standby 99 priority 110' | Increase priority value to make this switch HSRP active |
| 'standby 99 preempt' | Allows higher priority device to reclaim active status |
| 'interface vlan 10' | enters vlan configuration |
| 'standby 10 ip 10.10.03' | Add HSRP Virtual IP |
| 'standby 10 priority 110' | Increase priority values to make this switch active |
| 'standby 10 preempt' | Allows higher priority device to reclaim active status after the device or link comes up from failure |