

\# Navigating the Cisco IOS through CLI using Cisco Packet Tracer



\## 1. Project Overview



This project demonstrates the skills necessary for navigating the Cisco IOS, including different user access modes, various configuration modes, and common commands used on regular basis.

The goal is to demonstrate how to access a Cisco device, move between command modes, find help, inspect device status, and save a configuration.



\## 2. Objectives



&#x20;- Basic Connections, Accessing the CLI and exploring help

&#x20;- Exploring EXEC Modes, Setting passwords, password encryption and banner message




\## 3. Lab Environment



&#x20;- Simulation tool : Cisco Packet Tracer

&#x20;- Networking device : Cisco 2960 switch and a PC





\## 4. Implementation Steps and key learnings



1. Added one cisco 2960 switch and a pc
2. Connected PC to the switch using console cable (PC: RS-232, Switch: console)





\## 5. Key learnings and commands



On the PC, Selected Desktop>>Terminal, accepted the default settings and click OK. The Cisco CLI is accessed with prompt:

Switch>

This is **User EXEC** mode.



Tried commands (one at a time):



Switch> e?

Switch> c?

Switch> te?

displays available commands beginning with the letters. This is context-sensitive help, providing more information as the commands expand.



Commands below took to the **Privileged EXEC mode** and **Global Configuration mode** repectively:



Switch> enable				\*\* en for short

Switch#					\*\* this is Privileged mode

Switch# Configuration terminal		\*\* conf t for short

Switch(config)#				\*\* this is global configuration mode



In the global configuration mode, device-wide settings can be changed.

Switch(config)# int fa 0/1		\*\* enter interface configuration mode

Switch(config-if)# exit			\*\* return to global config mode

Switch(config)# end			\*\* return to Privileged EXEC mode



\*\* exit moves back one level, end or Ctrl+Z returns directly to Privileged EXEC mode. disable moves from Privileged EXEC to User EXEC mode.



Explored the following commands:



switch> en

switch# config t

switch(config)# hostname S1				\*\* named switch to S1

S1(config)# enable secret cisco				\*\* set privileged EXEC mode password

S1(config)# line console 0				\*\* enters console line configuration

S1(config-line)# password class				\*\* set user EXEC mode password

S1(config-line)# login					\*\* enforce the password to access the console

S1(config-line)# exit					\*\* return to global config mode

S1(config)# service password-encryption			\*\* encrypt passwords in the configuration

S1(config)# banner motd #Authorized access only!#	\*\* Configure login warning banner

S1(config)# end						\*\* back to user EXEC mode

S1# show run						\*\* show running configuration

S1# copy run start					\*\* save running configuration to startup configuration



|Commands			|	What it does or tells		|



show version				displays IOS version, hardware, uptime

show running-configuration		Configuration currently active in memory

show startup-configuration		Configuration saved for startup

show interfaces status			port status and vlan assignments

show mac address-table			MAC addresses learned by the switch

show ip interface brief			interface IP and status summary

