# Project_02: Optimizing Network Subnetting and Configuration for Site Expansion
Author: [Carl Xymon Verdejo](https://hardworking-lion-z4sd3b.mystrikingly.com/) </br>
Contact: [carl.xymon.verdejo@gmail.com](carl.xymon.verdejo@gmail.com)

# Project Overview
## Background
The aim of this project is to **extend** a previously configured small-scale network with multiple subnets and internet connectivity using Cisco Packet Tracer. Building upon the previous project ([Project_01](https://github.com/caxylive/CCNA-01-Subnetting-Network-Configuration-and-Management)), we will extend and conserve IP addresses for network expansion in Project_02.

## Network Topology (Pre-Subnetting)
The initial network topology in ([Project_01](https://github.com/caxylive/CCNA-01-Subnetting-Network-Configuration-and-Management)) consisted of two primary sites, Site_01 and Site_02, connected to an intermediary router (IntRouter) for internet access. Subnetting was performed on the ```192.168.1.0 /24``` network to allocate IP addresses efficiently for various network segments. In project_02, Site_03 along with a serial link to IntRouter was added which will warrant additional configuration.
![Figure 1: Network Topology](/screenshot/project_02-network-topology-initial.png)

## Objectives
1. Break up the ```192.168.1.64 /26``` subnet to support as many subnets as possible with at least 8 hosts each.
2. Allocate the first new subnet to Site_03 and manually configure all devices in this subnet.
3. Subnet the last network obtained from ```192.168.1.64/26``` with ```/30``` masks for serial links.
    - The subnets obtained from subnetting ```192.168.1.64/24``` are:
      - ```192.168.1.64 /28```
      - ```192.168.1.80 /28```
      - ```192.168.1.96 /28```
      - ```192.168.1.112 /28``` --> This is the last subnet. Therefore, this will be subnetted using /30 mask.
    - Take note that ```192.168.1.128 /28``` already belongs to the next block and is no longer part of the ```192.168.1.64/24``` block.
4. Verify network connectivity and internet access for all PCs.

# Network Design: Subnetting Calculations
![Table 1: Subnetting Table](/screenshot/project_02-subnetting-table.png)

# Network Design: Network Topology (After Subnetting)
After subnetting, the network was expanded to include Site_03. The new topology consists of three primary sites, each connected to the IntRouter, with subnets allocated for efficient IP address management. Below is a screenshot of the network topology populated with IP Addresses:
![Figure 2: Network Topology](/screenshot/project_02-network-topology.png)

## Site_03 (Subnet: 192.168.1.64/28)
| **Device**    | **IP Address**| CIDR | Interface        | ID    |
|---------------|---------------|------|------------------|-------|
| **PC6**       | 192.168.1.65  | /28  | FastEthernet     | 0     |
| **PC7**       | 192.168.1.66  | /28  | FastEthernet     | 0     |
| **PC8**       | 192.168.1.67  | /28  | FastEthernet     | 0     |
| **Switch S3** | 192.168.1.77  | /28  | Vlan             | 1     |
| **Router R4** | 192.168.1.78  | /28  | GigabitEthernet  | 0/0/0 |
| **Broadcast** | 192.168.1.79  | /28  |                  |       |

## Serial Links (Subnet: 192.168.1.112/30 - 192.168.1.120/30)
| **Link**             |**Network**        |**Router IP Address**   | **IP Address IntRouter** | **Directed Broadcast Address**|
|----------------------|-------------------|------------------------|--------------------------|-------------------------------|
| **R1 ↔ IntRouter**   | 192.168.1.112 /30 | 192.168.1.113 /30      | 192.168.1.114 /30        | 192.168.1.115 /30             |
| **R4 ↔ IntRouter**   | 192.168.1.116 /30 | 192.168.1.117 /30      | 192.168.1.118 /30        | 192.168.1.119 /30             |
| **R2 ↔ IntRouter**   | 192.168.1.120 /30 | 192.168.1.121 /30      | 192.168.1.122 /30        | 192.168.1.123 /30             |


# Device Configuration
## Router (R1) Serial Configuration Example
- Assign ```192.168.1.113``` ```255.255.255.252``` to R1 Serial 0/1/0 interface
- Bring up the interface: ```no shutdown```
- Check Serial 0/1/0 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 3: R1 Config - Serial 0/1/0](/screenshot/R1-config-serial.png)

## Router (R2) Serial Configuration Example:
- Assign ```192.168.1.121``` ```255.255.255.252``` to R2 Serial 0/1/0 interface
- Bring up the interface: ```no shutdown```
- Check Serial 0/1/0 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 4: R2 Config - Serial 0/1/0](/screenshot/R2-config-serial.png)

## Router (R4) Serial Configuration Example:
- Assign ```192.168.1.117``` ```255.255.255.252``` to R4 Serial 0/1/0 interface
- Bring up the interface: ```no shutdown```
- Check Serial 0/1/0 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 5: R4 Config - Serial 0/1/0](/screenshot/R4-config-serial.png)

## IntRouter ↔ R1 Serial Configuration Example:
- Assign ```192.168.1.114``` ```255.255.255.252``` to R1 Serial 0/1/0 interface
- Bring up the interface: ```no shutdown```
- Check Serial 0/1/0 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 6: IntRouter-R1 - Serial 0/1/0](/screenshot/IntRouter-config-serial-r1.png)

### IntRouter ↔ R2 Serial Configuration Example:
- Assign ```192.168.1.122``` ```255.255.255.252``` to R1 Serial 0/1/1 interface
- Bring up the interface: ```no shutdown```
- Check Serial 0/1/1 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 7: IntRouter-R2 - Serial 0/1/1](/screenshot/IntRouter-config-serial-r2.png)

## IntRouter ↔ R4 Serial Configuration Example:
- Assign ```192.168.1.118``` ```255.255.255.252``` to R1 Serial 0/2/0 interface
- Bring up the interface: ```no shutdown```
- Check Serial 0/2/0 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 8: IntRouter-R4 Config - Serial 0/2/0](/screenshot/IntRouter-config-serial-r4.png)

## R4 ↔ S3 GigabitEthernet Configuration Example:
- Assign ```192.168.1.78``` ```255.255.255.240``` to R4 GigabitEthernet 0/0/0 interface
- Bring up the interface: ```no shutdown```
- Check GigabitEthernet 0/0/0 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 9: R4↔S3 Config - GigabitEthernet 0/0/0](/screenshot/R4-config-r4-s3.png)

## S3 Vlan1 Configuration Example:
- Assign ```192.168.1.77``` ```255.255.255.240``` to S3 Vlan1 interface
- Bring up the interface: ```no shutdown```
- Check Vlan1 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 10: S3 Config - Vlan1](/screenshot/S3-config-vlan1.png)
### PS:
- Not shown in the screenshot above but S3's default gateway needs to be set to R4: ```ip default-gateway 192.168.1.78```

## Manually Configuring IPs for PCs
| PC       | IP Address     | Subnet Mask     | Default Gateway |
|----------|----------------|-----------------|-----------------|
| **PC6**  | 192.168.1.65   | 255.255.255.240 | 192.168.1.78    |
| **PC7**  | 192.168.1.66   | 255.255.255.240 | 192.168.1.78    |
| **PC8**  | 192.168.1.67   | 255.255.255.240 | 192.168.1.78    |

### PC6 Example (if using Windows cmd / PowerShell):
- Please note that cmd in Packet Tracer is limited and does not reflect the real-world cmd commands
- Also the GUI config in Packet Tracer is very different from the real-world GUI especially in Windows 11, Linux, and macOSX
- Refer to each Operating System's way of configuring their Network Interfaces
- The commands below **will NOT work** in Packet Tracer but will work on Windows 11 (real-world vs simulation):
``` cmd
netsh interface ipv4 set address name="FastEthernet0" static 192.168.1.65 255.255.255.240
netsh interface ipv4 set address name="FastEthernet0" gateway=192.168.1.78
netsh interface ipv4 set dns name="FastEthernet0" static 8.8.8.8
```
#### Note:
-```8.8.8.8``` is Google's Domain Name System server. Another well-known Google DNS is ```8.8.4.4```.

### PC7 **Example** (if using Ubuntu Linux):
- Open Terminal
- Edit the NetPlan Configuration File:
``` bash
sudo nano /etc/netplan/01-netcfg.yaml
```
- Add the Network Configuration:
``` Yaml
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: no
      addresses:
        - 192.168.1.66/28
      gateway4: 192.168.1.78
      nameservers:
        addresses:
          - 8.8.8.8
```
- Apply the Configuration:
``` bash
sudo netplan apply
```
- Verify the configuration:
``` bash
ip a
```

### PC8 **Example** (if using macOSX)
- Open Terminal
- Find the Network Interface Name and identify the network interface you want to configure:
``` bash
networksetup -listallnetworkservices
```
- Set the IP Address and Subnet Mask:
``` bash
sudo networksetup -setmanual FasthEthernet0 192.168.1.67 255.255.255.240
```
- Set the Default Gateway:
``` bash
sudo route add default 192.168.1.78
```
- Set the DNS Server:
``` bash
sudo networksetup -setdnsservers FastEthernet0 8.8.8.8
```

# Verification and Testing
To verify the network configuration, several tests were conducted:

## Ping Tests:
- PCs were able to ping their default gateways and other devices within their subnet.
- PCs successfully pinged external IP addresses (e.g., Google DNS [8.8.8.8], facebook.com, cisco.com).
![Figure 11: Pinging External Sites](/screenshot/PC6-ipconfig-ping.png)
- Pinging Internal Devices from Site_01 and Site_02 </br>
![Figure 12: Pinging Internal Devices](/screenshot/PC6-ping.png)

### PS:
- Connectivity tests are not limited to the screenshots shown above.
- Please test every single device on your network one-by-one.

## Browser Tests:
- Just type the URL (Uniform Resource Locator) into a browser's address bar.
- PCs accessed websites like [cisco.com](cisco.com)
![Figure 13: Visiting Cisco's Website](/screenshot/PC6-cisco.png)
- And [facebook.com](facebook.com) to confirm internet connectivity.
![Figure 14: Visiting Facebook's Website](/screenshot/PC6-facebook.png)

# Results
The ```192.168.1.64 /26``` subnet was successfully divided into smaller subnets, maximizing the number of subnets with at least 8 hosts each. This approach allowed for efficient IP address allocation and accommodated additional devices within the network.

The first new subnet ```192.168.1.64 /28``` was allocated to Site_03. All devices in Site_03, including Router R4, Switch S3, and PCs (PC6, PC7, and PC8), were manually configured with appropriate IP addresses. This ensured that Site_03 was fully integrated into the network.

The last new subnet from ```192.168.1.64 /26``` was further divided into ```/30``` subnets for serial links. This provided efficient IP address allocation for the serial links connecting R4, R2, and R1 to the IntRouter. Each serial link was configured with the correct IP addresses, ensuring seamless connectivity.

Extensive verification and testing were conducted to ensure network connectivity and internet access for all PCs. Ping tests confirmed that PCs could communicate with their default gateways and other devices within their subnets. Browser tests verified that PCs could access external websites like [cisco.com](cisco.com) and [facebook.com](facebook.com), demonstrating successful internet connectivity.

The project successfully met all the objectives, demonstrating the effectiveness of subnetting and IP address management. The network's scalability and manageability were enhanced, providing a solid foundation for future expansion and optimization.

# Limitations of Project
## 1. Simulation Tool Constraints
Cisco Packet Tracer is a simulation tool and does not fully replicate real-world network behavior in terms of performance, latency, and security threats.

## 2. Lack of Redundancy
The current setup lacks redundancy mechanisms such as HSRP, VRRP, or load balancing, which are crucial for enterprise-level reliability.

## 3. Minimal Security Measures
Security configurations like firewall rules and access control lists (ACLs) were not implemented in this project.

## 4. Limited ```cmd``` and ```terminal``` Commands
Commands used for Windows PowerShell, Linux Terminal, and macOSX terminal will probably not work in Packet Tracer. Please practice using the real-world terminal. For Packet Tracer, just use their GUI when possible. 
I provided different examples from different Operating Systems (under the Device Configuration section) on how to configure network settings.

# Future Improvements and Optimization
## 1. Implementing Redundancy and Failover Mechanisms
Introduce protocols like **HSRP** or **VRRP** to ensure failover if a router goes down. Use **EtherChannel** or **Link Aggregation** (**LACP**) to create redundant links.

## 2. Optimizing Network Performance
Implement **Quality of Service** (**QoS**) to prioritize critical traffic. Introduce **traffic shaping** and **rate limiting** to prevent congestion.

## 3. Enhancing Security Measures
Apply **ACLs** on routers to restrict unauthorized traffic. Implement **firewall rules** and **802.1X authentication** for device access control. Enable **IDS/IPS** for network monitoring.

## 4. Expanding the Network with VLANs and Subnetting
Introduce **VLAN segmentation** to improve security and reduce broadcast traffic. Use **Inter-VLAN Routing** to enable communication between different VLANs.

## 5. Real-World Deployment and Testing
Conduct **physical implementation** using real routers, switches, and servers to test **real-world performance**. Use tools like **GNS3** or **EVE-NG** for more accurate network simulations. Perform **penetration testing** to evaluate network security.

# Conclusion
The project successfully demonstrated the implementation of a structured enterprise-level network using subnetting, routing, switching, and DHCP services. By dividing the ```192.168.1.0/24``` network into smaller subnets, IP address management was optimized, and logical segmentation was achieved. The configuration of routers, switches, and DHCP servers ensured efficient network communication between local and remote hosts. This topology serves as a foundational model for small-to-medium business networks, providing scalability and efficiency while maintaining security and performance. Future improvements could include VLAN segmentation, load balancing, and redundancy mechanisms to improve fault tolerance. Overall, the project achieved its goals and laid the groundwork for a robust and scalable network infrastructure.

