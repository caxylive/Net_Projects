# **Inter-Site Connectivity Using EIGRP in a Subnetted Network**

---

## **1. Introduction**
This project demonstrates the implementation of **EIGRP** to establish dynamic routing between two geographically separated networks: San Francisco (`192.168.1.0/26`) and New York (`192.168.1.64/26`). Prior to EIGRP configuration, inter-site communication was unavailable due to the absence of routing protocol-driven route propagation. By configuring EIGRP, full connectivity was achieved, enabling seamless data transfer between sites.

---

### **Technologies Used**
- **Dynamic Routing**: EIGRP (Enhanced Interior Gateway Routing Protocol)
- **IP Addressing**: Subnetting, VLSM (Variable Length Subnet Masking), CIDR
- **Network Services**: DHCP, DNS (simulated)
- **Tools**: Cisco IOS, Cisco Packet Tracer

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
```Cisco IOS
ip dhcp pool NY
 network 192.168.1.64 255.255.255.192
 default-router 192.168.1.126
ip dhcp excluded-address 192.168.1.126
ip name-server 192.168.1.126
```

![**Figure 4**: R2 DHCP and DNS Configuration](screenshot/003/config-r2-dhcp-dns.png)  
*DHCP pool setup and DNS configuration on R2.*

Note: In production environments, DNS is typically hosted on a dedicated server. Here, R2 simulates DNS resolution for testing purposes.

---

## **4. EIGRP Implementation**
#### **Configuration on R1 and R2**
```Cisco IOS
router eigrp 100
 network 192.168.1.0
 no auto-summary
```

![**Figure 5**: EIGRP Configuration on R1](screenshot/003/config-r1-eigrp.png)  
*EIGRP setup for the San Fransisco subnet (AS 100).*

---

### Verification

1. Neighbor Adjacency
The ```show ip eigrp neighbors``` command confirms successful adjacency between R1 and R2:

![**Figure 6**: EIGRP Neighbor Status](screenshot/003/r1-show-ip-eigrp-beighbors.png)
*Stable neighbor relationship indicated by increasing uptime and ```Q Count = 0```.*

---

2. Routing Tables
Post-EIGRP routing tables show dynamically learned routes:

![**Figure 7**: Post-EIGRP Routing Table on R1]()
*```D``` (EIGRP) routes for remote subnets, confirming route propagation.*

---

## **5. Testing and Validation**
### **Pre-EIGRP Connectivity**
- ❌ Inter-site pings failed due to missing routes:  
  ![**Figure 8**: Failed Inter-Site Ping](screenshot/003/inter-site_ping_fail.png)  
  *Ping from San Francisco to New York before EIGRP configuration.*

---

### **Post-EIGRP Connectivity**
- ✅ **Successful Inter-Site Pings**  
  ![**Figure 9**: Successful Inter-Site Ping](screenshot/003/ping_success.png)  
  *Ping from PC1 (San Francisco) to PC2 (New York) after EIGRP convergence.*

---

- **Summary of Critical Tests**
  | Source          | Destination     | Result  |
  |-----------------|-----------------|---------|
  | PC1 (SF)        | PC2 (NY)        | Success |
  | R1 (SF)         | R2 (NY) WAN     | Success |
  | S1 (SF)         | S2 (NY)         | Success |

> Full connectivity was validated across all devices. [View detailed test log](#).

---

## **6. Conclusion**
EIGRP was successfully implemented to automate route propagation between San Francisco and New York, eliminating reliance on static routes. Key outcomes include:
- **Dynamic Scalability**: Simplified expansion to additional subnets.
- **Efficient Convergence**: Sub-second route updates during topology changes.
- **Reduced Overhead**: No manual route maintenance required.

**Future Enhancements**:  
- Redundancy testing with backup links.
- Comparative analysis with OSPF.

## **7. Appendix: Key Concepts**
### **EIGRP (Enhanced Interior Gateway Routing Protocol)**
- **Protocol Type**: Advanced distance-vector (hybrid).
- **Key Features**: Fast convergence, support for VLSM/CIDR, unequal-cost load balancing.
- **Autonomous System (AS)**: Routers within the same AS (e.g., AS 100) exchange routing updates.

---

### **DHCP Pool**
- **Purpose**: Dynamically assign IP addresses, gateways, and DNS settings.
- **Exclusions**: Reserved addresses (e.g., `ip dhcp excluded-address 192.168.1.126`).

---

### **Autonomous System (AS) Number**
- **Purpose**: Identifies the EIGRP process and ensures routers within the same AS exchange routing information.
- **Example**: Both R1 and R2 were configured with `router eigrp 100` to establish adjacency.









