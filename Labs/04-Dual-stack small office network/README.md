Dual-Stack Small office network

1. Project Overview

This project focuses on designing and implementing a dual-stack small office network using cisco packet tracer.
The network uses both IPV4 and IPV6 to demonstrate how devices communicate across different network segments through routers and switches. In addition to configuring the network, i used Pcaket Tracer Simulation mode to study how data travels through network, including OSI layers, PDUs, encapsulation and decapsulation.


2. Objectives

The main objective was to build a functional network, understand how the networks devices  and services communicate, understand the PDUs, TCP and UDP and verify the results through practical testing.

3. Lab Environment
Simulation tool: Cisco Packet Tracer

4. Network Topology
The network consists of three main areas: Administration department, Central server network and Technical department. All three network connect through a Cisco ISR4331 router.

5. IPv4 and IPv6 addressing table
   
   Administration Department: 
                           IPv4  - 192.168.0.0/24
                           IPv6  - 2001:db8:acad:10::/64
   
   Technical Department:
                           IPv4  - 192.168.2.0/24
                           IPv6  - 2001:db8:acad:20::/64

   Central Server:
                           IPv4  - 192.168.3.0/29
                           IPv6  - 2001:db8:acad:30::/64

Two departments have seperate DHCP servers, while DNS, web and FTP servers are hosted centrally.

6. Services and Protocols
 IPv4 and IPv6
   - configured IPv4 addressing for the network segments
   - configured IPv6 addressing for dual-stack communication
   - used IPv6 Router Advertisements and SLAAC for automatic IPv6 configuration. While using DHCPv6 in generic server-PT device in cisco packet tracer, I encountered a limitation. In my testing, configuring the generic server for DHCPv6 caused unexpected Router Advertisement behaviour, including clients receiving an incorrect default gateway. To avoid this issue, I did not use DHCPv6 in this project.

 DHCP
   - Configured a dedicated DHCP server for each department
   - Using Simulation Mode, PDU details were inspected across the four-step DORA (Discover, offer, request, ACK) handshake over UDP ports(67/68), tracking layer 2-7 header  encapsulation from initial client broadcast through final IPv4 lease acknowledgment.
   - verified that clients in the respective departments received IPv4 configuration automatically.

 DNS
   Configured DNS records for both IPv4 and IPv6:
   - A records map hostnames to IPv4 address
   - AAAA records map hostnames to IPv6 address.

   Configured records for network services:
    - smalloffice
    - smalloffice.com
    - www.smalloffice.com
    - ftp.smalloffice.com
    - dns.smalloffice.com

   DNS resolution was tested from the departments. Screenshots show the configured A and AAAA records.

 HTTP/HTTPS and FTP
   HTTP/HTTPS access tested. Verified the TCP 3-way handshake (SYN, SYN-ACK, ACK) over port 443 via PDU inspection in Simulation mode, tracking layer 4 sequence/acknowledgment numbers and control flags prior to encrypted HTTPS session establishment. Inspected UDP data transmission, confirming connectionless layer 4 encapsulation using destination IP and ports without handshake, sequence tracking or delivery acknowledgments.
   FTP service was also provided with the same central server. For FTP service, two seperate user accounts were configured with username and passwords for authentication. Individual account were configured with the permissions for file operations. 


7. PDU Analysis, OSI Models and Encapsulation
An important objective was to understand what happens to data as it moves through the network -- not only how to configure the devices. The Cisco Packet Tracer Simulation Mode was used to inspect PDUs and follow communication between network devices. I investigated how the encapsulation occurs at every layers of OSI model and observed how protocol information changes as data moves between devices. The investigation includes:
      - ARP PDUs at multiple devices like hosts, switch and routers.
      - DNS queries and responses.
      - HTTP(Port 80) and HTTPs(Port 443) request and response PDUs.
      - FTP PDUs and how the large files are transported over TCP with Handshake negotiations, MSS(maximum segment size) and MTU(maximum transmission unit).
This helped connect OSI model and protocol theory with observable network behaviour.

8. Learning Outcomes
   This project gave me practical experience designing, configuring, testing and troublshooting a small-office dual-stack network. It strengthened my understanding of IPv4 and IPv6, routing, DHCP, DNS, web and FTP services and how data is encapsulated and forwarded through network devices.
   The project helped me connect theoretical networking concepts- especially the OSI models and PDUs--with practical observations in cisco Packet Tracer.
