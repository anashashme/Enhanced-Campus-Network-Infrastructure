**Enhanced Campus Networking System**  
**Overview**  
The Enhanced Campus Networking System project is designed to establish a robust and efficient network infrastructure for a campus environment. Utilizing VLANs, DHCP, GRE tunnels, and ACLs, this project ensures secure, segmented, and efficient communication across various departments and blocks within the campus. This repository contains the detailed network design, configuration files, and step-by-step instructions for replicating the setup.

**Network Design**  
The campus network is divided into five main blocks: A, B, C, D, and E. Each block is further segmented into departments, each with its own VLAN to manage network traffic efficiently.

**Block A**
Departments: Admin, HR, Finance, Help Desk  
VLANs:  
VLAN 10 (192.168.1.0/24) - Admin Dept  
VLAN 20 (192.168.2.0/24) - HR Dept  
VLAN 30 (192.168.3.0/24) - Finance Dept  
VLAN 40 (192.168.4.0/24) - Help Desk  
Switches: Four 2960-24TT switches connected to an L3 switch, which uplinks to Router 2911.

**Block B**
Departments: Computing, Bio-Medical  
VLANs:  
VLAN 50 (192.168.5.0/24) - Computing  
VLAN 60 (192.168.6.0/24) - Bio-Medical  
Switches: Two 2960-24TT switches connected to an L3 switch, which uplinks to Router 2911.  

**Block C**
Departments: IT Department, Student Lab  
VLANs:  
VLAN 70 (192.168.7.0/24) - IT Dept  
VLAN 80 (192.168.8.0/24) - Student Lab  
Servers: Web Server and DNS Server  
Switches: Two 2960-24TT switches connected to an L3 switch, which uplinks to Router 2911.  

**Block D**  
Department: Staff  
VLANs:  
VLAN 90 (192.168.9.0/24)  
Switches: One 2960-24TT switch connected to an L3 switch, which uplinks to Router 2911.  

**Block E**  
Department: Student Lab  
VLANs:  
VLAN 100 (192.168.10.0/24)  
Switches: One 2960-24TT switch connected to an L3 switch, which uplinks to Router 2911.  

**Key Technologies**
VLANs: Used for network segmentation to manage traffic efficiently.  
DHCP: Dynamic Host Configuration Protocol ensures dynamic IP address allocation.  
GRE Tunnels: Generic Routing Encapsulation used for secure and efficient inter-router communication.  
ACLs: Access Control Lists to control the flow of traffic between VLANs and ensure network security.  

**Configuration Files**
The repository includes configuration files for:  

VLAN setup on switches.  
DHCP configuration on routers.  
GRE tunnel configuration between routers.  
ACL configuration for traffic control.  
Instructions  

**Setting Up VLANs on Switches**  
Connect to the switch using a console cable.  
Enter the following commands to create and assign VLANs:  
Switch> enable  
Switch# configure terminal  
Switch(config)# vlan 10  
Switch(config-vlan)# name Admin_Dept  
Switch(config-vlan)# exit  

**Configuring DHCP on Routers**  
Connect to the router using a console cable.  
Enter the following commands to configure DHCP pools:  
Router> enable  
Router# configure terminal  
Router(config)# ip dhcp pool VLAN10  
Router(dhcp-config)# network 192.168.1.0 255.255.255.0  
Router(dhcp-config)# default-router 192.168.1.1  
Router(dhcp-config)# dns-server 8.8.8.8  
Router(dhcp-config)# exit  

**Setting Up GRE Tunnels**  
Connect to the router using a console cable.  
Enter the following commands to configure GRE tunnels:   
Router> enable  
Router# configure terminal  
Router(config)# interface tunnel 0   
Router(config-if)# ip address 10.10.10.1 255.255.255.252  
Router(config-if)# tunnel source 192.168.12.1  
Router(config-if)# tunnel destination 192.168.12.2  
Router(config-if)# exit  
Configuring ACLs  
Connect to the router using a console cable.  
Enter the following commands to create and apply ACLs to control traffic:  
plaintext  
Copy code  
Router> enable  
Router# configure terminal  
Router(config)# access-list 100 permit ip 192.168.1.0 0.0.0.255 any  
Router(config)# access-list 100 deny ip 192.168.2.0 0.0.0.255 any  
Router(config)# interface gigabitEthernet 0/0  
Router(config-if)# ip access-group 100 in  
Router(config-if)# exit  

**Testing and Verification**
Each PC was tested for connectivity across different VLANs and blocks to ensure proper network segmentation and functionality. Pings were successful both within the same router's network and across different routers' networks, confirming the correct configuration of VLANs, DHCP, GRE tunnels, and ACLs.

**Conclusion**
The Enhanced Campus Networking System project successfully implemented a scalable and efficient network infrastructure using VLANs, DHCP, GRE tunnels, and ACLs. The network design ensures secure and segmented communication across various departments and blocks, meeting the campus's needs.

**License**
This project is licensed under the Apache 2.0 License - see the LICENSE file for details.
