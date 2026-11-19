# CCNA Command Reference



A personal  reference of Cisco IOS command learned during CCNA studies.



This document records commands, their purpose, and where they are commonly used.







## 1. Basic Cisco IOS Navigation



| `Command` | What it does |
| --- | --- |
| `enable` | Enters privileged EXEC mode(#). |
| `disable` | Returns to user EXEC mode(>). |
| `configure terminal` | Enters global configuration mode. |
| `exit` | moves back one config level. |
| `end` | returns directly to privileged EXEC mode |





## 2. Basic Router and Switch Settings

| `command` | what it does |
| --- | --- |
| `hostname *name-of-device*` |	Name the device. |
| `enable secret *encrypted-password-to-set*` | sets encrypted password required to enter privileged EXEC mode. |
| `service password-encryption` | encrypts plaintext passwords in the running configuration. |
| `banner motd "message of the day"` | displays a warning or information to users before they access the device. |
| `security passwords min-length` | sets minimum number of characters required for newly configured passwords. |
| `login block-for *180 attempts* 3 within *60*` | blocks login for 180 seconds after 3 failed attempts within 60 seconds. |
| `no ip domain-lookup` | disables DNS lookup when an unrecognized command is entered, preventing the device from trying to resolve it as a hostname. |



**Configure a console line password**

| `command` | what it does |
| --- | --- |
| `line console 0` | Enters console line configuration mode to configure console access. |
| `password *Cisco*` | sets the password (Cisco) for console access. |
| `login` | enables password authentication when accessing the console line. |
| `exec-timeout 4 0` | sets idle session timeout to 4 minutes and 0 seconds. |


**Configure a VTY line password (Remote access)**

| `command` | what it does |
| --- | --- |
| `line vty 0 4` | Enters VTY line config mode for lines 0-4, used for remote access. The available VTY range depends on the device, check with *show line*. |
| `password *Cisco*` | sets the password (Cisco) for remote access. |
| `login` | enables the password authentication when accessing remotely. |
| `exec-timeout 3 30` | sets idle session timeout to 3 minutes and 30 seconds. |


**Remote access configuration (SSH)**

| `command` | what it does |
| --- | --- |
| `ip domain-name *domain.com*` | configures the domain name required for RSA key generation. |
| `username *Admin* secret *Cisco*` | creates a local user account with an encrypted password. |
| `crypto key generate rsa` | Generates RSA key required for SSH connection. |
| `ip ssh version 2` | enables ssh version 2. |
| `login local` | uses the local username database for authentication. |
| `transport input ssh` | allows SSH connection on the VTY lines and blocks other remote access protocols. |


**Configure interfaces (common commands for router and switch)**

| `command` | what it does |
| --- | --- |
| `int *interface-id(f0/0, g0/0, g0/0/0)*` | enters interface configuration mode to configure a specific interface. |
| `int range *interface-id(f0/0-5, g0/0-2)*` | selects multiple interfaces for simultaneous configuration. |
| `description *Admin LAN*` | adds description to the interface. |
| `no shut` | enables the interface. |
| `shutdown` | administratively disables the interface. |
| `speed *100*` | manually sets the interface speed to 100Mbps, if supported. |
| `speed auto` | enables automatic speed negotiation. |
| `duplex *full/half/auto*` | enables full duplex, half duplex and automatic negotiation. |
| `midx auto` | enables automatic MDI/MDIX detection, if supported. |


**Router-Specific Interface Configuration**

| `command` | what it does |
| --- | --- |
| `ipv6 unicast-routing` | in the global configuration mode, enables ipv6 packet forwarding between networks. |
| `ip add *192.168.1.20 255.255.255.0*` | assigns an IPv4 address and subnet mask to an interface. |
| `no ip address` | removes an IPv4 address from the interface. |
| `ipv6 enable` | enables IPv6 on an interface and generates a link-local address. It is must if the interface does not have an explicit IPv6 address. |
| `ipv6 add *2001:db8:1::1/64*` | assigns an explicit IPv6 address to an interface. |
| `ipv6 add *fe80::1* link-local` | manually assigns a link-local IPv6 address. |
| `int loopback 0` | creates or enters a virtual loopback interface. |


**Switch-specific Interface Configuration**

A layer 2 switch primarily forwards network traffic using MAC address and does not have an IP address assigned to its physical interfaces. Unlike a router, which can be accessed remotely through an IP address, a switch requires a management SVI and a default gateway for remote access.


| `command` | what it does |
| --- | --- |
| `int vlan *1*` | enters the SVI configuration mode for VLAN 1. |
| `ip add *192.168.1.2 255.255.255.0*` | Assigns an IPv4 management address to the SVI. |
| `ip default-gateway *192.168.1.1*` | Defines the gateway used to reach devices outside the management subnet. Default-gateway is assigned in global config mode, not SVI config mode. |




## 3. VLAN Configuration

| `command` | what it does |
| --- | --- |
| `vlan 10` | creates VLAN with VLAN id 10 and enters VLAN config mode |
| `name *Admin*` | Assigns the name Admin to VLAN 10 |


Access port carries the traffic for one VLAN while Trunk port carries traffic for multiple VLANs. Access port is used in between switch and end devices and trunk port is used in between network devices, usually switches. Trunk port uses VLAN tagging (IEEE 802.1q) to identify which VLAN each Ethernet frame belongs to.


**Access port configuration**

| `command` | what it does |
| --- | --- |
| `int *f0/0*` | Enters interface config mode. (interface f0/0 here). |
| `switchport mode access` | configures the interface as an access port. |
| `switchport access vlan 10` | Assigns the interface to VLAN 10. |
| `switchport voice vlan 20` | Assigns voice traffic to VLAN 20. VLAN 20 must be created beforehand to assign for voice traffic. |

**Trunk port configuration** 

| `command` || what it does |
| --- | --- |
| `int *f0/0*` | enters interface config mode. |
| `switchport mode trunk` | configures the interface as trunk port. |
| `switchport trunk encapsulation dot1q` | Specifies IEEE 802.1Q encapsulation, where supported. Many modern cisco switches support only 802.1Q, so the encapsulation command may not be necessary or not available at all. |
| `switchport trunk allowed vlan 10,20` | by default, trunk allows all VLANs. this command restricts all VLANs and allowed the specified VLANs only. |
| `switchport trunk allowed vlan {add/remove} 10` | this command adds or removes the allowed VLAN without changing the other VLANs permission. |
| `switchport trunk native vlan 99` | Native VLAN is the VLAN whose traffic is transmitted untagged across a trunk link. Native VLAN should match on both ends of a trunk link to avoid native VLAN mismatch. by default, VLAN 1 is the native VLAN on cisco switches. this command changes the native VLAN on the trunk port to VLAN 99|

**DTP Configuration**

Dynamic Trunking Protocol (DTP) is a cisco proprietary protocol that allows switches to negotiate whether a link should operate as a trunk. It perfectly works in between cisco networking devices, but might not work with other vendors. Its always best to manually configure trunk ports while working with multi-vendor devices.

| `command` | what it does |
| --- | --- |
| `int f0/0` | enters interface config mode. |
| `switchport mode dynamic auto` | Makes the interface passively wait for other side to initiate trunk negotiation. this is also default configuration. |
| `switchport mode dynamic desirable` | Actively attempts to negotiate a trunk connection. |
| `switchport nonegotiate` | Disables DTP negotiation on the interface. It is good to configure this command when the port is access port or manually configured trunk port. |

| modes on two ends of connection | what it makes |
| --- | --- |
| dynamic auto + dynamic auto | Access Link |
| dynamic auto + dynamic desirable | Trunk Link |
| dynamic desirable + dynamic desirable | Trunk Link |

## 4. Inter-VLAN Routing

Inter-VLAN routing allows devices in different VLANs to communicate with each other through a layer 3 device, such as router or layer 3 switch.

** Router-On-A-Stick (ROAS)**

This method uses a single physical router interface connected to a switch trunk port. The router uses multiple sub-interfaces to route traffic between VLANs. A sub-interface is a logical interface created within physical interface. Each sub-interface handles traffic for a specific VLAN and acts as that VLANs default gateway.

| `command` | what it does |
| --- | --- |
| `int g0/0` | selects the physical router interface connected to the switch |
| `no ip address` | removes any IPv4 address configured on the physical interface. For ROAS, we remove IP address from physical interface because IP address will be assigned to sub-interfaces. |
| `no shut` | enables the physical interface |

**Router sub-interface Configuration**

| `command` | what it does |
| --- | --- |
| `int g0/0.10` | Creates and enters sub-interface 10 under physical interface g0/0. The sub-interface number is 10 in g0/0.10, it does not need to match exactly with VLAN ID. |
| `encapsulation dot1q 10` | Associates the sub-interface with VLAN 10 using IEEE 802.1Q tagging. Number 10, in encapsulation dot1q 10, needs to match exactly with the VLAN ID. |
| `ip address 192.168.10.1 255.255.255.0` | Assigns the default gateway IP address for VLAN 10. |
| `int g0/0.20` | creates and enters sub-interface 20. |
| `encapsulation dot1q 20` | Associates the sub-interface with VLAN 20. |
| `ip add 192.168.20.1 255.255.255.0` | Assigns the default gateway IP address for VLAN 20. |