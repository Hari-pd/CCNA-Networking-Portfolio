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



