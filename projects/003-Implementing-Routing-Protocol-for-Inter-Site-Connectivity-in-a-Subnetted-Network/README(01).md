# **Inter-Site Connectivity Using EIGRP in a Subnetted Network**

## **Technologies Used**
- **Dynamic Routing**: EIGRP (Enhanced Interior Gateway Routing Protocol)
- **IP Addressing**: Subnetting, VLSM (Variable Length Subnet Masking), CIDR
- **Network Services**: DHCP, DNS (simulated)
- **Tools**: Cisco IOS, Cisco Packet Tracer

---

## **1. Introduction**
This project demonstrates the implementation of **EIGRP** to establish dynamic routing between two geographically separated networks: San Francisco (`192.168.1.0/26`) and New York (`192.168.1.64/26`). Prior to EIGRP configuration, inter-site communication was unavailable due to the absence of routing protocol-driven route propagation. By configuring EIGRP, full connectivity was achieved, enabling seamless data transfer between sites.

---

## **2. Network Design**
### **Subnetting Scheme**
The `192.168.1.0/24` address space was subdivided as follows:
- **San Francisco LAN**: `192.168.1.0/26` (60 host addresses)
- **New York LAN**: `192.168.1.64/26` (60 host addresses)
- **WAN Link**: `192.168.1.128/30` (point-to-point serial connection)

![**Figure 1**: Network Topology](screenshot/003/network_topology-00.png)  
*Logical topology showing subnets and device interconnections.*

![**Figure 2**: Subnet Allocation Table](screenshot/003/subnetting_table.png)  
*Subnet ranges and address assignments.*

---

## **3. Device Configurations**
### **San Francisco Router (R1)**
#### **Interface Configuration**
| Description               | Command                                      |
|---------------------------|----------------------------------------------|
| Configure LAN Interface   | `interface GigabitEthernet0/0/0`             |
| Assign IP Address         | `ip address 192.168.1.62 255.255.255.192`   |
| Configure WAN Interface   | `interface Serial0/1/0`                      |
| Assign IP Address         | `ip address 192.168.1.129 255.255.255.252`  |

![**Figure 3**: R1 Interface Configuration](screenshot/003/config-r1_initial.png)  
*Relevant interface commands and verification output on R1.*

---

### **New York Router (R2)**
#### **DHCP and DNS Configuration**
```bash
ip dhcp pool NY
 network 192.168.1.64 255.255.255.192
 default-router 192.168.1.126
ip dhcp excluded-address 192.168.1.126
ip name-server 192.168.1.126
