#### **IPV4 Routing Using OSPF**



1. **Project Overview**

&#x09;This project demonstrates basic IPV4 network configuration and dynamic routing using Open Shortest Path First (OSPF) in cisco packet tracer. 

The network consist of two Cisco 1941 routers connected through a point-to-point serial WAN link. Each router connects to two separate private LAN networks through switches. OSPF is configured in both routers to enable dynamic route exchange and communication between all four private LAN networks.



2\. **Project Objectives**:

&#x09;- Configure IPV4 address in router interfaces

&#x09;- Configure private LAN networks and WAN connections

&#x09;- Implement OSPF dynamic routing

&#x09;- Configure OSPF using interface-level commands

&#x09;- Configure passive interfaces to control OSPF Hello Packets

&#x09;- Verify connectivity between remote networks



**3. Network Topology**

&#x09;The topology consists of five IPV4 networks:

&#x09;	-four private LAN networks

&#x09;	-one point-to-point WAN network connecting two routers

&#x09;Network design:

&#x09;	R1 - LAN-1 >> 192.168.10.0/24

&#x09;	R1 - LAN-2 >> 192.168.11.0/24

&#x09;	R1 - R2    >> 209.165.200.224/30

&#x09;	R2 - LAN-3 >> 10.1.1.0/24

&#x09;	R2 - LAN-4 >> 10.1.2.0/24



**4. OSPF configuration**

&#x09;OSPF is used as the dynamic routing protocol to exchange routing information between R1 and R2. Both routers operates in area 0. 



&#x09;**Router1 (R1):**

&#x09;	router ospf 1			: Starts ospf process 1

&#x09;	router-id 1.1.1.1		: Assigning a unique router id

&#x09;	passive-interface default	: Makes all interfaces passive by default to control HELLO Packets.

&#x09;	no passive-interface s0/1/0	: Allows OSPF HELLO packets in WAN interface

&#x09;	int s0/1/0			: enters interface configuration mode

&#x09;	ip ospf 1 area 0		: enables OSPF on the specified interface in area 0



The OSPF is enabled in all interfaces in R1 and R2. The WAN interface links the router to external networks through other routers for adjacencies, dynamic route exchange and link failure detection. Because of this reason, the link can not be set passive. 

The OSPF process ids are different on R1 and R2 because the process ids are locally significant and does not need to match between routers.



**5. Verification and testing**

&#x09;The following commands were used for verifying the configuration.

&#x09;	show ip interface brief		: check interface status

&#x09;	show ip ospf neighbour		: check OSPF neighbours

&#x09;	show ip route ospf		: check OSPF routing information

&#x09;	show ip protocols		: check OSPF configuration

&#x09;	ping 192.168.10.10		: test connectivity between LANS

&#x09;	tracert 192.168.10.10		: check the route



**Note: Security configuration are intentionally no included!**



**6. Learning Outcomes:**

&#x09;Through this project, i practised:

&#x09;	- Designing a small network with multiple LAN segments.

&#x09;	- Configuring IPV4 addresses on router interfaces.

&#x09;	- Implementing OSPF using interface-level configuration

&#x09;	- Understanding OSPF process id, router id and area 0.

&#x09;	- Using passive interfaces to control OSPF neighbour relationships and CPU usage.

&#x09;	- Verifying routing tables and connectivity.

