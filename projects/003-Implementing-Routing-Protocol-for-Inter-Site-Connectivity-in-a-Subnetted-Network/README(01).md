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
### **San Francisco Router (R1) and New York Router (R2) Initial Configuration**
#### **Interface Configuration**
| Description               | Command (R1)                                 | Command (R2)                               |
|---------------------------|----------------------------------------------|--------------------------------------------|
| Configure LAN Interface   | `interface GigabitEthernet0/0/0`             | `interface GigabitEthernet0/0/0`           |
| Assign IP Address         | `ip address 192.168.1.62 255.255.255.192`    | `ip address 192.168.1.126 255.255.255.192`  |
| Bring interface up        | `no shutdown`                                | `no shutdown`                              |
| Configure WAN Interface   | `interface Serial0/1/0`                      | `interface Serial0/1/0`                    |
| Assign IP Address         | `ip address 192.168.1.129 255.255.255.252`   | `ip address 192.168.1.130 255.255.255.252` |
| Bring interface up        | `no shutdown`                                | `no shutdown`                              |
| Write changes from vRAM to nvRAM | `copy running-config startup-config`  | `copy running-config startup-config`       |

![**Figure 3**: R1 Interface Configuration](screenshot/003/config-r1_initial.png)  
*Relevant interface commands and verification output on R1.*

---

### **San Francisco Switch (S1) and New York Switch (S2)**
#### **Interface Configuration**
| Description               | Command (S1)                                 | Command (S2)                              |
|---------------------------|----------------------------------------------|-------------------------------------------|
| Configure LAN Interface   | `interface vlan1`                            | `interface vlan1`                         |
| Assign IP Address         | `ip address 192.168.1.61 255.255.255.192`    | `ip address 192.168.1.61 255.255.255.192` |
| Bring interface up        | `no shutdown`                                | `no shutdown`                             |
| Set Default Gateway       | `ip default-gateway 192.168.1.62`            | `ip default-gateway 192.168.1.126`        | 
| Verify configuration      | `show ip interface brief`                    | `show ip interface brief`                 |
| Write changes from vRAM to nvRAM | `copy running-config startup-config`  | `copy running-config startup-config`      |

![**Figure 4**: Switch (S1) and (S2) Configuration](screenshot/003/config-switch_initial.png)  
*Relevant interface commands and verification output on S1.*

---

### **New York Router (R2)**
#### **DHCP and DNS Configuration**
```Cisco IOS
ip dhcp pool NY
 network 192.168.1.64 255.255.255.192
 default-router 192.168.1.126
ip dhcp excluded-address 192.168.1.125 192.168.1.127
ip name-server 192.168.1.126
```

![**Figure 5**: R2 DHCP and DNS Configuration](screenshot/003/config-r2-show-run.png)  
*DHCP pool setup and DNS configuration on R2.*

**Note**: 
- In production environments, DNS is typically hosted on a dedicated server. Here, R2 simulates DNS resolution for testing purposes.
- `default-router` → Used in DHCP to tell clients which router to use as their gateway.
-  `ip default-gateway` → Only used on switches or routers with IP routing disabled (not needed here).
-  R2 does not need `ip default-gateway` because it's a router, and routing protocols take care of forwarding traffic.
-  **DHCP Pool** enables the DHCP server to automatically assign IP addresseses based on this "pool" of addresses, reducing the workload and minimizing errors.
-  By excluding IP addresses (`ip dhcp excluded-address 192.168.1.125 192.168.1.127`), R2 avoids assigning the IP addresses of itself, S2, and broadcast IP to the hosts.

---

## **4. EIGRP Implementation**
#### **Configuration on R1 and R2**
```Cisco IOS
router eigrp 100
 network 192.168.1.0
 no auto-summary
```

![**Figure 6**: EIGRP Configuration on R1](screenshot/003/config-r1-eigrp.png)  
*EIGRP setup for the San Fransisco subnet (AS 100).*

Note:
- By default, EIGRP autonatically summarizes routes at classful nework boundaries. This means EIGRP will summarize and advertise only the classful network address, potentially leading to inaccuracies in routing.
- For example, EIGRP might summarize and advertise subnets within the `192.168.1.0/24` network (such as `192.168.1.0/26` and `192.168.1.64/26`) as `192.168.1.0/24` → leading to incorrect routing.
- The `no auto-summary` command disables automatic summarization, ensuring that EIGRP advertises the specific subnets rather than summarizing them at classful boundaries → more accurate routing info.

---

### Verification <a id="verification"></a>

1. **Neighbor Adjacency** <a id="verification-neighbor-adjacency"></a>

The ```show ip eigrp neighbors``` command confirms successful adjacency between R1 and R2:
- Uptime increasing means that the adjacency is stable.
- `Q count = 0` means that there are no pending EIGRP updates waiting to be sent.

![**Figure 7**: EIGRP Neighbor Status](screenshot/003/r1-show-ip-eigrp-beighbors.png)
*Stable neighbor relationship indicated by increasing uptime and ```Q Count = 0```.*

---

2. **Routing Tables** <a id="verification-routing-tables"></a>

Post-EIGRP routing tables show EIGRP is correctly exchanging and installing routes between R1 and R2:
- The `D` EIGRP code appears in R1 and R2's routing table. This means that EIGRP is learning routes dynamically.
- San Francisco Subnet `192.168.1.0/26` is reachable via EIGRP from R2 through R1's Serial Interface `192.168.1.129/30`.
- New York Subnet `192.168.1.64/26` is also reachable via EIGRP from R1 through R2's Serial Interface `192.168.1.130/30`.

  ![**Figure 8**: Post-EIGRP Routing Table on R1 and R2](screenshot/003/output-show_ip_route.png)
  *```D``` (EIGRP) routes for remote subnets, confirming route propagation.*

---

## **5. Testing and Validation**
### **Pre-EIGRP Connectivity**
- ❌ Inter-site pings failed due to missing routes:  

  ![**Figure 9**: Failed Inter-Site Ping](screenshot/003/inter-site_ping_fail.png)  
  *Ping from San Francisco to New York before EIGRP configuration.*

---

### Pre-EIGRP Routing Tables

  ![**Figure 10**: No EIGRP Routes](screenshot/003/pre-eigrp-routing-tables.png)  

The routing tables does not show any `D` EIGRP entries, which means that R1 **has not learned any routes** from R2 via EIGRP and vice versa. The only entries are for directly connected subnets (`C`) and local addresses (`L`), meaning R1 is not receiving updates from R2 and vice versa.

---

### Post-EIGRP Routing Tables
Please revisit the [verification](#verification-routing-tables) section to view the results after the routing tables have been configured with EIGRP.

---

### **Post-EIGRP Connectivity**
- ✅ **Successful Inter-Site Pings**

  ![**Figure 10**: Successful Inter-Site Ping](screenshot/003/ping_success.png)  
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

EIGRP was successfully implemented to automate route propagation between the San Francisco and New York sites. Through dynamic routing, EIGRP enabled automatic route learning and sharing, eliminating the need for static routes. Key outcomes include simplified expansion to additional subnets, sub-second route updates during topology changes, and elimination of manual route maintenance. Future enhancements could include redundancy testing with backup links and comparisons with alternative routing protocols such as OSPF.







