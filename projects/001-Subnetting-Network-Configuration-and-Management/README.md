# Subnetting, Network Configuration and Management
**Author**: [**Carl Xymon Verdejo**](https://hardworking-lion-z4sd3b.mystrikingly.com/)</br>
**Contact**: carl.xymon.verdejo@gmail.com

## **1. Project Overview**
### Background
You have been allocated subnet 192.168.1.0/24 and is tasked to subdivide it into four networks.

### Network Topology:
- Each LAN in this network topology is connected to a switch, specifically a **3650-24PS model**, which facilitates communication among the devices within that network segment. 
- The routers, **ISR4321 models**, act as gateways between the LANs and the broader network, handling inter-subnet routing and external connectivity. 
- Both routers, **Routr1 (R1)** and **Router2 (R2)**, use **GigabitEthernet interfaces** for their LAN connections and **Serial interfaces** for their WAN links to the Internet Router. 
- The Internet Router (**IntRouter**), also an **ISR4321**, connects to both **Site 1** and **Site 2** via serial links and extends connectivity to the Internet via its **GigabitEthernet 0/0/1 interface**, which has **DHCP** enabled.

![Figure 1: Network Topology](/screenshot/001/network_topology-initial.png)

### Objectives
  - Design and configure a small-scale network with multiple subnets and internet connectivity. The allocated IP address range of **192.168.1.0/24** needs to be divided into four subnets:
      - **Subnet_1**: assigned to **Site_1**, which consists of multiple PCs, a server (Server1), a switch, and a **R1**.
      - **Subnet_2**: serves as a point-to-point link between **R1** and **IntRouter**, enabling communication between **Site_1** and **external networks**.
      - **Subnet_3**: assigned to **Site_2**, contains another set of PCs, a server (Server2), a switch (S2), and **R2**.
      - **Subnet_4**: serves as a point-to-point link between **R2** and **IntRouter**, ensuring connectivity for **Site_2**.
  - Configure Routers with the **Last IP Address** in the Subnet
  - For **Subnet_2** and **Subnet_4**: configure **R1** and **R2**'s **serial interface** with the **first IP Address** in the Subnet
  - Configure the Switches with the **second last IP Address** in the Subnet
  - Configure the DHCP Servers with the **third last IP Address** in the Subnet
  - Configure the DHCP Servers to dynamically allocate IP Addreses to the Clients
  - Verify that the PCs can access cicso.com and facebook.com using their browsers
- **Tools Used**: Cisco Packet Tracer

## **2. Network Design**
### Subnetting Calculations
Before configuring the devices, it is recommended to properly calculate and tabulate the IP Address of each devices. There will be a lot of **dynamic and static IP addresseses** on this network (much more so in the real world!) and one might easily misconfigure a device without proper documentation.

The table below shows the relationships between IP addresses and interfaces for each device on their respective subnets. It also shows how the binary format of each IP address looks like to easily understand which is the **Network Portion** and **Host Portion** of the each address.
![Figure 2: Subnetting Excel Spreadsheet](/screenshot/001/subnetting_details.png)

### Network Topology After Subnetting
This is how the network topology looks like after populating with labels according our the subnetting table. This way, it is easier to visualize the network and configure the devices.
![Figure 3: Network Topology Populated](/screenshot/001/network_topology-final.png)

## 3. Device Configuration
### Router R1
- Enable the **GigabitEthernet 0/0/0** interface using the ```no shutdown``` command
- Configure the **GigabitEthernet 0/0/0** interface with IP address ```192.168.1.62/26```
- Enable the **Serial 0/1/0** interface using the ```no shutdown``` command
- Configure the **Serial 0/1/0** interface with IP address ```192.168.1.66/26```
- Save the current running configuration to the startup configuration using the ```copy running-config startup-config``` command
![Figure 4: Router1 (R1) Configuration](/screenshot/001/configuration-R1-01.png)

### Router R2
- Enable the **GigabitEthernet 0/0/0** interface using the ```no shutdown``` command
- Configure the **GigabitEthernet 0/0/0** interface with IP address ```192.168.1.190/26```
- Enable the **Serial 0/1/0** interface using the ```no shutdown``` command
- Configure the **Serial 0/1/0** interface with IP address ```192.168.1.193/26```
- Save the current running configuration to the startup configuration using the ```copy running-config startup-config``` command
![Figure 5: Router2 (R2) Configuration](/screenshot/001/configuration-R2-01.png)

### Switch S1
- Configure the **Default Gateway** to **R1** ```192.168.1.62```
- Enable the **Vlan1** interface using the ```no shutdown``` command
- Configure the **VLAN1** interface with Second last IP address in the subnet ```192.168.1.61/26```
- Save the current running configuration to the startup configuration using the ```copy running-config startup-config``` command
- Verify interface is up using ```show ip interface brief```
![Figure 6: Switch1 (S1)](/screenshot/001/configuration_S1-01.png)

### Switch S2
- Enable the **Vlan1** interface using the ```no shutdown``` command
- Configure the **VLAN1** interface with Second last IP address in the subnet ```192.168.1.189/26```
- Configure the **Default Gateway** to **R2** ```192.168.1.190```
- Save the current running configuration to the startup configuration using the ```copy running-config startup-config``` command
- Verify interface is up using ```show ip interface brief```
![Figure 7: Switch2 (S2)](/screenshot/001/configuration_S2-01.png)

### DHCP Server1
- Configure Server1 with the 3rd last IP Address within the subnet ```192.168.1.60```
![Figure 8: DHCP Server1 - Global Settings](/screenshot/001/configuration_Server1-FastEthernet0-01.png)

- Set the Default Gateway to R1 ```192.168.1.62```
- Point the DNS to Google ```8.8.8.8```
![Figure 9: DHCP Server1 - FastEthernet0](/screenshot/001/configuration_Server1-globalSettings-01.png)

- Configure the DHCP Pool
- Refer back to the Subnetting Table to determine the IP range for this subnet
- The amount of users that can connect to this network can also be set here.
- Take note of all the Static IPs so that they can be excluded from the range.
![Figure 10: DHCP Server1 - DHCP_Pool](/screenshot/001/configuration_Server1-services-dhcp-01.png)

### DHCP Server2
- Configure Server1 with the 3rd last IP Address within the subnet ```192.168.1.188```
![Figure 11: DHCP Server1 - Global Settings](/screenshot/001/configuration_Server2-FastEthernet0-01.png)

- Set the Default Gateway to R2 ```192.168.1.190```
- Point the DNS to Google ```8.8.8.8```
![Figure 12: DHCP Server1 - FastEthernet0](/screenshot/001/configuration_Server2-globalSettings-01.png)

- Configure the DHCP Pool
- Refer back to the Subnetting Table to determine the IP range for this subnet
- The amount of users that can connect to this network can also be set here.
- Take note of all the Static IPs so that they can be excluded from the range.
![Figure 13: DHCP Server1 - DHCP_Pool](/screenshot/001/configuration_Server2-services-dhcp-01.png)

## **4. Important Notes:**
### The ```no shutdown``` Command
- **Enables** an interface that is **administratively down**.
- By default, many interfaces on Cico devices are in a "**shutdown**" state (i.e., they are **disabled** and not operational).
- This command brings the interface up, allowing it to start functioning and transmitting data.

### The ```copy running-config startup-config``` Command
- Saves the current running configuration (**the configuration in RAM**) to the startup configuration (**the configuration file in NVRAM**).
- Ensures the current configuration is preserved and will be used the next time the device reboots.
- Without this command, any changes made to the running configuration would be lost upon reboot.

### Interface Configuration: Routers vs Switches
- When configuring a router's interface, such as GigabitEthernet 0/0/0, you're dealing directly with a physical interface that connects to other network devices. This is why you configure the IP address directly on the GigabitEthernet interface.
- Switches, on the other hand, primarily operate at Layer 2 (the data link layer) of the OSI model, dealing with MAC addresses and Ethernet frames. However, for management purposes, switches can have a Layer 3 interface, which is typically configured on a VLAN interface. By default, VLAN 1 is the management VLAN on most switches.

### Why **VLAN 1** on the Switch instead of **GigabitEthernet**?
#### Management Interface
VLAN 1 is used to manage the switch itself, allowing you to configure settings, apply updates, and perform other administrative tasks.
#### IP Address Assignment
An IP address is assigned to VLAN 1 to enable remote management of the switch. This IP address is used to access the switch's management interface.
#### Physical Ports
The physical ports (GigabitEthernet) on the switch are still used to connect devices, but they do not typically have IP addresses assigned directly to them in a typical Layer 2 switch setup. Instead, they are associated with VLANs, which can then be managed through VLAN interfaces.
  - Devices (PC0, PC1, PC2, Server1) connected to switch ports (e.g., GigabitEthernet 0/0/1, 0/0/2, etc.), but these ports are part of VLAN 1, and their IP management is handled through the VLAN interface.
#### In summary
Configuring VLAN 1 on the switch with an IP address allows you to manage the switch, while the physical GigabitEthernet ports are used to connect devices without requiring individual IP addresses for each port.

## **5. Verification and Testing**
1. Verifying connectivity between all devices.
2. Test connectivity to external IP address ```8.8.8.8```
![Figure 13: DHCP Server1 - DHCP_Pool](/screenshot/001/test-ping.png)
3. Ensuring all PCs (PC0-PC5) can access external websites (e.g., cisco.com, facebook.com).
![Figure 13: DHCP Server1 - DHCP_Pool](/screenshot/001/test-pc0-facebook.png)

## **6. Results**
The network topology was successfully implemented and configured according to the design specifications. The subnetting scheme was correctly applied, ensuring efficient IP address allocation across the four designated subnets: 
- Site 1
- Site 2
- The link between R1 and the Internet Router
- The link between R2 and the Internet Router.

All networking devices, including routers, switches, and PCs, were configured with their respective IP addresses, and connectivity tests were conducted to verify proper communication. The DHCP servers at Site 1 and Site 2 successfully allocated dynamic IP addresses to client devices, confirming that the address distribution was functioning as intended.

Routing was established using static or dynamic routing protocols to enable seamless communication between the two LANs and external internet resources. Ping tests confirmed that devices from Site 1 could reach Site 2 and vice versa. Additionally, traceroute commands verified the correct path for network traffic.

To test internet connectivity, PCs attempted to access the simulated external servers (8.8.8.8, cisco.com, and facebook.com) using web browsers and ping requests. The successful responses confirmed that the Internet Router was properly forwarding traffic and that NAT (if configured) allowed internal devices to reach external networks.

Furthermore, network performance was assessed using tools such as Wireshark to monitor packet flows, ensuring no significant delays or packet loss occurred during transmission. Security measures were also reviewed, including access control lists (ACLs) and firewall settings to regulate traffic and prevent unauthorized access.

## **7. Limitations of the Project**
While the network topology was successfully implemented in Cisco Packet Tracer, there are certain limitations that need to be considered. 

### 1) **Real-world Network Behavior**
Packet Tracer is a simulation tool and does not fully replicate real-world network behavior, particularly in terms of:
  - Performance
  - Latency
  - Security Threats
  - Hardware Constraints </br>

Some advanced configurations, such as certain firewall rules, deep packet inspection, advanced VLAN management, and real-world routing protocols like BGP, are either not supported or only partially functional in Packet Tracer.

### 2) **Network Optimization**
The current setup does not include crucial mechanisms for enterprise-level reliability such as:
  - Load Balancing
  - Redundancy
  - Failover Protocols
  - Traffic Shaping </br>

If one of the routers in the topology were to fail, the entire communication pathway could be disrupted since no high-availability mechanisms like HSRP, VRRP, or dynamic routing failover were implemented.

### 3) **Minimal Security Features**
Safeguards from potential cyber threats are missing:
  - Firewall Configurations
  - Access Control Lists (ACLs)
  - Intrusion Detection/prevention Systems (IDS/IPS)</br>

In a real-world scenario, network security would be a primary concern, requiring more advanced encryption, authentication mechanisms, and monitoring tools like SNMP, Syslog, or SIEM solutions.

### 4) Additional Configurations
In this project, NAT and OSPF have already been preconfigured. In the real-world, more configurations are involved before being able to connect to other devices and the internet.

## **8. Future Improvements and Optimization**
To improve the network topology and bring it closer to real-world standards, the following enhancements can be considered:

### 1) Implementing Redundancy and Failover Mechanisms
- Introduce **Hot Standby Router Protocol** (**HSRP**) or **Virtual Router Redundancy Protocol** (**VRRP**) to ensure failover if a router goes down.
- Use **EtherChannel** or **Link Aggregation** (**LACP**) to create redundant links between switches and prevent single points of failure.
- Implement **multiple ISPs** or **multi-homed routing** to ensure internet access remains available even if one ISP connection fails.

### 2) Optimizing Network Performance
- Implement **Quality of Service** (**QoS**) to prioritize critical traffic such as voice or video communication.
- Introduce **traffic shaping** and **rate limiting** to prevent network congestion.
- Configure **load balancing** across routers to distribute network traffic more efficiently.

### 3) Enhancing Security Measures
- Apply **Access Control Lists** (**ACLs**) on routers to restrict unauthorized traffic.
- Implement **firewall rules** to protect against external attacks.
- Configure 802.1X authentication for device access control.
- Enable **Intrusion Detection** and Prevention Systems** (**IDS/IPS**) for network monitoring.

### 4) Expanding the Network with VLANs and Subnetting
- Introduce **VLAN segmentation** to improve security and reduce broadcast traffic.
- Use **Inter-VLAN Routing** to enable communication between different VLANs.
- Further subnet the network to optimize IP address allocation and improve security.

### 5) Real-World Deployment and Testing
- Conduct physical implementation using real routers, switches, and servers to test real-world latency, hardware limitations, and performance.
- Use **GNS3**, **EVE-NG**, or actual Cisco hardware instead of Packet Tracer to simulate a more accurate network environment.
- Perform **penetration testing** to evaluate network security and identify vulnerabilities.

By addressing these limitations and implementing the suggested improvements, the network can be more scalable, secure, and reliable, making it better suited for real-world business environments.

## **9. Conclusion**
The project successfully demonstrated the implementation of a structured enterprise-level network using subnetting, routing, switching, and DHCP services. By effectively dividing the ```192.168.1.0/24``` network into smaller subnets, IP address management was optimized, and logical segmentation was achieved.

The configuration of routers, switches, and DHCP servers ensured efficient network communication between local and remote hosts. The ability of the PCs to reach both internal and external servers confirmed that the routing tables and internet access settings were correctly implemented.

This network topology serves as a foundational model for small-to-medium business networks, providing scalability and efficiency while maintaining security and performance. Future improvements could include VLAN segmentation for enhanced security, load balancing for better traffic distribution, and redundancy mechanisms such as HSRP or VRRP to improve fault tolerance.

Overall, the project was a success, demonstrating practical networking concepts and reinforcing the principles of network design, IP subnetting, and connectivity troubleshooting.

