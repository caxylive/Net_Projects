# **Implementing EIGRP for Inter-Site Connectivity in a Subnetted Network**

## **1. Introduction**
In modern network infrastructures, efficient routing is essential to ensure seamless communication between different sites. This project involves configuring and implementing the Enhanced Interior Gateway Routing Protocol (EIGRP) to enable full network connectivity between two locations: San Francisco and New York. Prior to configuring EIGRP, devices within each site could communicate locally, but inter-site communication was not possible. The goal of this project is to enable dynamic routing using EIGRP so that devices from both sites can reach each other efficiently.

## **2. Network Design**
The network has been subnetted using the `192.168.1.0/24` address space. To accomodate the required 60 hosts per subnet, San Francisco and New York each utilize a `/26` subnet, while the serial link connecting the two sites operates on a `/30` subnet to avoid wasting IP addresses. The addressing scheme is as follows:
![Network Topology](/screenshot/003/network_topology-00.png)
- **San Francisco (`192.168.1.0/26`)**
  - **PC1**: `192.168.1.1` (Static IP)
  - **PC2**: `192.168.1.2` (Static IP)
  - **Switch (S1)**: `192.168.1.61`
  - **Router (R1)**: `192.168.1.62`

- **New York (`192.168.1.64/26`)**
  - **PC3**: `192.168.1.65` (DHCP)
  - **PC4**: `192.168.1.66` (DHCP)
  - **Switch (S2)**: `192.168.1.125`
  - **Router (R2)**: `192.168.1.126`

- **San Francisco - New York Link (`192.168.1.128/30`)**
  - **R1 (SF Side)**: `192.168.1.129`
  - **R2 (NY Side)**: `192.168.1.130`

## **3. Initial Device Configurations**
While the focus of this project is on EIGRP, key device configurations are included to highlight network setup differences. 

### **San Francisco R1 (Static IP Configuration)**
- Select R1's G0/0/0 interface: ```interface GigabitEthernet 0/0/0```
- Assign IP Address and Subnet Mask: ```ip address 192.168.1.62 255.255.255.192```
- Bring the interface up: ```no shutdown```
- Select R1's Serial 0/1/0 interface: ```interface Serial 0/1/0```
- Assign IP Address and Subnet Mask: ```ip address 192.168.1.129 255.255.255.252```
- Bring up the interface: ```no shutdown```
- Check IP and Interface table and ensure interfaces are administratively up:```do show ip interface brief```
- Write changes from vRAM to nvRAM: ```copy running-config startup-config``` or ```wr```
![San Francisco R1 Initial Configuration](/screenshot/003/config-r1_initial.png)

### San Fransisco S1
- Select Vlan1 on S1: ```interface vlan1```
- Assign IP Address and Subnet Mask: ```ip address 192.168.1.61 255.255.255.192```
- Bring the interface up: ```no shutdown```
- Verify with the interface summary: ```do show ip interface brief```
- Save the configuration: ```copy running-config startup-config``` or ```wr```
![San Fransisco S1 Configuration](/screenshot/003/config-s1_initial.png)

### **New York R2: Initial Configuration**
- Select R2's GigabitEthernet 0/0/0 interface: ```interface g0/0/0```
- Assign IP Address and Subnet Mask: ```ip address 192.168.1.130 255.255.255.252```
- Bring the interface up: ```no shutdown```
- Verify with the interface summary: ```do show ip interface brief```
- Save the configuration from vRAM to nvRAM: ```copy running-config startup-config```
![New York R2 Initial Configuration](/screenshot/003/config-r2_initial.png)

### New York S2
- Select S2's Vlan1 interface: ```interface vlan1```
- Assign IP Address and Subnet Mask: ```ip address 192.168.1.125 255.255.255.192```
- Set default gateway to R2: ```ip default-gateway 192.168.1.26```
![New York S2 Initial Configuration](/screenshot/003/config-s2_initial.png)
- Verify Vlan1 is administratively up with assigned IP address:```do show ip interface brief```
![New York S2 Show Interface](/screenshot/003/config-s2_interface.png)
- Check the running configuration to verify default gateway assignment: ```do show run```
![New York S2 Default Gateway](/screenshot/003/config-s2_defaultGateway.png)
- Save the configuration: ```copy running-config startup-config```

### New York R2: DHCP and DNS Configuration
- Assign a name to the DHCP Pool: ```ip dhcp pool NY```
- Specify the network address and subnet mask for the DHCP pool: ```network 192.168.1.64 255.255.255.192```
- Ensure the DHCP Server does not assign its own IP address to other devices: ```ip dhcp excluded-address 192.168.1.126```
- Set the default gateway to R2: ```ip default-gateway 192.168.1.126```
- Specify the DNS server's IP address: ```ip name server 192.168.1.126```
  - Please note that in the real-world, there will be a separate DNS server.
![New York R2 DHCP, Default Gateway, and DNS Configuration](/screenshot/003/config-r2_dhcp-defaultGateway-dns.png)
- Verify the DHCP pool, excluded addresses, default gateway, and DNS server: ```do show run```
![New Yor R2 Show Running Configuration](screenshot/003/config-r2_show-run.png)
- Save the running config once everything is ok: ```copy running-config startup-config```

## **4. EIGRP Configuration**
Since devices in San Francisco could not initially communicate with devices in New York, EIGRP was implemented to dynamically share routing information.

### **Configuring EIGRP on R1 (San Francisco Router)**
```bash
router eigrp 100
 network 192.168.1.0 0.0.0.63
 network 192.168.1.128 0.0.0.3
 no auto-summary
```
![R1 EIGRP Configuration](/screenshot/003/r1_eigrp.png)

### **Configuring EIGRP on R2 (New York Router)**
```bash
router eigrp 100
 network 192.168.1.64 0.0.0.63
 network 192.168.1.128 0.0.0.3
 no auto-summary
```
![R2 EIGRP Configuration](/screenshot/003/r2_eigrp.png)

## **5. Testing and Verification**
### **Pre-EIGRP Configuration Test Results**
Before configuring EIGRP:
- Devices within San Francisco and within New York could ping each other.
- San Francisco devices could not reach New York devices, and vice versa.
![Communication Failed](/screenshot/003/ping_fail.png)

### **Post-EIGRP Configuration Test Results**
After implementing EIGRP:
- `show ip route` confirmed that EIGRP dynamically shared routes.
- Devices in San Francisco successfully pinged devices in New York.
- Devices in New York successfully pinged devices in San Francisco.
![Communication Successful](/screenshot/003/ping_success.png)

Example verification command:
```bash
ping 192.168.1.65
```
Expected successful response.

### Routing Table
#### R1 Routing Table After EIGRP
![R1 Routing Table](/screenshot/003/r1_routing_table.png)

#### R2 Routing Table After EIGRP
![R2 Routing Table](/screenshot/003/r2_routing_table.png)

## **6. Conclusion**
This project successfully demonstrated the implementation of EIGRP to achieve full connectivity between the San Francisco and New York sites. Through dynamic routing, EIGRP enabled automatic route learning and sharing, eliminating the need for static routes. Future enhancements could include redundancy testing and comparisons with alternative routing protocols such as OSPF.

