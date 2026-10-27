
# Small Office LAN — IP Addressing and Connectivity Testing

## 1. Project Overview

This project demonstrates how to build and test a small local area network (LAN) using Cisco Packet Tracer.

The goal is to configure IPv4 addresses, connect multiple PCs through a switch, and verify connectivity using the ping command.

## 2. Objectives

- Build a simple switched LAN.
- Configure static IPv4 addresses.
- Understand subnet masks and network membership.
- Test connectivity between devices.
- Document the network topology and test results.

## 3. Lab Environment

- **Simulation tool:** Cisco Packet Tracer
- **Network devices:** 1 Cisco 2960 switch and 4 PCs
- **Network type:** Local Area Network (LAN)
- **Addressing method:** Static IPv4 addressing

## 4. IP Addressing Plan

| Device | IPv4 Address | Subnet Mask |
|---|---|---|
| PC0 | 192.168.1.7 | 255.255.255.0 |
| PC1 | 192.168.1.8 | 255.255.255.0 |
| PC2 | 192.168.1.9 | 255.255.255.0 |
| PC3 | 192.168.1.10 | 255.255.255.0 |

**Network address:** 192.168.1.0/24

**Default gateway:** Not configured; this lab does not include a router.

## 5. Implementation Steps

1. Added one Cisco 2960 switch and four PCs.
2. Connected each PC to the switch using copper straight-through cables.
3. Configured static IPv4 addresses and subnet masks.
4. Tested connectivity between PCs using ping.
5. Saved the Packet Tracer topology and screenshots.

## 6. Verification

Example commands executed from PC0:


ping 192.168.1.8
ping 192.168.1.9
ping 192.168.1.10


**Actual test results:** 
Successful ping results.

## 7. Key Learnings

- A switch forwards Ethernet frames within a LAN using MAC addresses.
- Devices in the same IPv4 subnet can communicate directly when correctly configured.
- ARP helps a device discover the MAC address associated with a local IPv4 destination.
- Ping uses ICMP messages to test IP connectivity.

## 8. Project Files

- `myfirstproject.pkt` — Packet Tracer network simulation.
- `screenshots/` — Network topology and connectivity test evidence.

## 9. Future Improvements

- Configure VLANs to separate network traffic.
- Introduce DHCP for automatic IP address assignment.
- Add a router and configure inter-VLAN routing.
- Practise troubleshooting incorrect IP addresses and subnet masks.
