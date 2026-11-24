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



