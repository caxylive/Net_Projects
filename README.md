<a name="top"></a>
# My Networking Projects

---

**Author**: [**Carl Xymon Verdejo**](https://hardworking-lion-z4sd3b.mystrikingly.com/)</br>
**Contact**: carl.xymon.verdejo@gmail.com

---

This repository serves as a collection of networking projects designed to enhance my technical knowledge and practical skills in IT. Each project focuses on key networking concepts such as subnetting, routing, and network configuration, reinforcing my understanding as I progress in my IT journey.

---
## Table of Contents
|Project Number | Project Title                                                                                                                                   |
|:-------------:|-------------------------------------------------------------------------------------------------------------------------------------------------|
| 001           | [Subnetting, Network Configuration and Management](#1-subnetting-network-configuration-and-management)                                          |
| 002           | [Optimizing Network Subnetting and Configuration for Site Expansion](#2-optimizing-network-subnetting-and-configuration-for-site-expansion)     |
| 003           | [Inter-Site Connectivity Using EIGRP in a Subnetted Network](#3-inter-site-connectivity-using-eigrp-in-a-subnetted-network)                     |
| 004           | [Wireshark Network Analysis](#4-wireshark-network-analysis)                                                                                                                   |

---

## 1) [Subnetting, Network Configuration and Management](https://github.com/caxylive/Net_Projects/tree/main/projects/001%20-%20Subnetting%20Network%20Configuration%20and%20Management)
This project focuses on subnetting an allocated network into smaller subnets to accommodate multiple network segments. I configured IP addressing, set up devices for internal communication, and enabled external network access. The goal was to design a scalable and well-organized network that supports efficient IP address allocation, reduces waste, and ensures seamless connectivity within and outside of subnets.

**Tools Used**:
- Cisco Packet Tracer
- Routers, Switches, VLANs

Key Challenges & Solutions:
- **Challenge**: Determining the correct subnet mask and network size for each segment, ensuring efficient use of IP space.
  - **Solution**: Applied VLSM (Variable Length Subnet Masking) to optimize subnet sizes based on the number of devices in each subnet.
- **Challenge**: Ensuring connectivity between different subnets without running into IP address conflicts.
  - **Solution**: Configured routing and device interfaces to ensure each subnet could communicate with others and maintain an active internet connection.

[Back to Top](#top)

---

## 2) [Optimizing Network Subnetting and Configuration for Site Expansion](https://github.com/caxylive/Net_Projects/tree/main/projects/002%20-%20Optimizing%20Network%20Subnetting%20and%20Configuration%20for%20Site%20Expansion)
As organizations grow, their networks must expand to accommodate new devices and sites. This project optimizes a previous network design to add a new site while maintaining efficient IP address utilization. The focus is on adjusting network configurations to seamlessly integrate the new site, ensuring no connectivity issues arise while optimizing the use of IP addresses.

**Tools Used**:
- Cisco Packet Tracer
- Routers, Switches, VLANs, Routing Protocols (OSPF or EIGRP depending on the setup)

**Key Challenges & Solutions**:
- **Challenge**: Managing IP address allocation while expanding the network for an additional site.
  - **Solution**: Carefully planned subnetting to accommodate the new site and integrated it without IP conflicts.
- **Challenge**: Ensuring the network scales without causing bottlenecks or inefficiencies.
  - **Solution**: Configured routing protocols to facilitate smooth communication between the sites, prioritizing efficiency and redundancy.

[Back to Top](#top)

---

## 3) [Inter-Site Connectivity Using EIGRP in a Subnetted Network](https://github.com/caxylive/Net_Projects/tree/main/projects/003%20-%20Inter-Site%20Connectivity%20Using%20EIGRP%20in%20a%20Subnetted%20Network)
This project demonstrates the configuration of Enhanced Interior Gateway Routing Protocol (EIGRP) to establish dynamic routing between two geographically separate sites: San Francisco and New York. By implementing EIGRP, the previously isolated sites can communicate with one another efficiently.

Before implementing EIGRP, the two sites could not communicate due to the lack of a routing protocol to propagate routing information between them. The goal of the project was to enable dynamic routing and facilitate seamless communication between sites, thus eliminating the need for manual static routing.

**Technologies Used**:
- **Dynamic Routing Protocol**: EIGRP (Enhanced Interior Gateway Routing Protocol)
- **Subnetting**: VLSM (Variable Length Subnet Masking)
- **Network Services**: DHCP (Dynamic Host Configuration Protocol), DNS (simulated)
- **Tools**: Cisco Packet Tracer, Cisco IOS

**Key Challenges & Solutions**:
- **Challenge**: Ensuring that the EIGRP routing protocol correctly advertised subnet routes to both sites.
  - **Solution**: Proper EIGRP configuration, including the assignment of an Autonomous System (AS) number and ensuring no automatic summarization of subnets using no auto-summary.
- **Challenge**: Ensuring both sites could assign IPs dynamically to devices without IP conflicts.
  - **Solution**: Implemented a DHCP server on the New York router (R2) and configured static IPs on San Francisco devices, ensuring all IP assignments were correctly allocated.
- **Challenge**: Verifying that both sites could reach each other after EIGRP was configured.
  - **Solution**: Ran connectivity tests (ping) from both sites and validated EIGRP route propagation using routing table commands and neighbor relationships.

[Back to Top](#top)

---

## 4) [Wireshark Network Analysis](https://github.com/caxylive/Net_Projects/tree/main/projects/005%20-%20Wireshark%20Network%20Analysis)
These series of projects document my learning journey with Wireshark, focusing on network traffic analysis for security forensics and understanding fundamental networking protocols. It includes analysis of HTTP, DNS, and other network traffic using Wireshark. Each sub-project documents the steps taken, observations, challenges, and key learnings. View the individual sub-projects here:
      
  1. [HTTP Analysis](https://github.com/caxylive/Net_Projects/blob/main/projects/005%20-%20Wireshark%20Network%20Analysis/Project-5-VoIP-Analysis/README.md)
      
  2. [Malware Detection](https://github.com/caxylive/Net_Projects/blob/main/projects/005%20-%20Wireshark%20Network%20Analysis/Project-2-Malware-Detection/)
  
  3. [Intrusion Detection](https://github.com/caxylive/Net_Projects/blob/main/projects/005%20-%20Wireshark%20Network%20Analysis/Project-3-Intrusion-Detection/)

  4. [TLS Decryption](https://github.com/caxylive/Net_Projects/blob/main/projects/005%20-%20Wireshark%20Network%20Analysis/Project-4-TLS-Decryption/)

  5. [VoIP Analysis](https://github.com/caxylive/Net_Projects/blob/main/projects/005%20-%20Wireshark%20Network%20Analysis/Project-5-VoIP-Analysis/)

[Back to Top](#top)

---
