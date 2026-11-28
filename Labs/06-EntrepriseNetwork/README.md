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

For redundancy, two layer-3 switches were used. STP and HSRP configured to prevent switching loops and redundancy. For First layer-3 switch, the name is give HQ-SW-1. Applied IP address and it's respective interfaces are:

| interface | IP address | Purpose |
| VLAN 10 |

## 5. IP address allocation

**IPv4 allocation**

| VLAN | Name | Network | Default Gateway |
| --- | --- | --- | --- |
| 10 | Admin | 10.10.0.0/26 | 10.10.0.3 |
| 20 | HR | 10.10.0.64/26 | 10.10.0.67 |
| 30 | IT | 10.10.1.0/26 | 10.10.1.3 |
| 40 | Sales | 10.10.1.64/26 | 10.10.1.67 |
| 50 | CS-and-Sec | 10.10.1.128/26 | 10.10.1.131 |
| 60 | GUEST-CONNECT | 10.10.60.0/24 | 10.10.60.3 |
| 99 | Mgmt | 10.10.99.0/24 | 10.10.99.5 |
| 101 | SRV | 10.10.10.0/26 | 10.10.10.5 |