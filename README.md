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

## 1) [Subnetting, Network Configuration and Management](https://github.com/caxylive/Net_Projects/tree/main/projects/001%20-%20Subnetting%20Network%20Configuration%20and%20Management/README.md)
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

## 2) [Optimizing Network Subnetting and Configuration for Site Expansion](https://github.com/caxylive/Net_Projects/tree/main/projects/002%20-%20Optimizing%20Network%20Subnetting%20and%20Configuration%20for%20Site%20Expansion/README.md)
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

## 3) [Inter-Site Connectivity Using EIGRP in a Subnetted Network](https://github.com/caxylive/Net_Projects/tree/main/projects/003%20-%20Inter-Site%20Connectivity%20Using%20EIGRP%20in%20a%20Subnetted%20Network/README.md)
This project demonstrates the configuration of Enhanced Interior Gateway Routing Protocol (EIGRP) to establish dynamic routing between two geographically separate sites: San Francisco and New York. By implementing EIGRP, the previously isolated sites can communicate with one another efficiently.

Before implementing EIGRP, the two sites could not communicate due to the lack of a routing protocol to propagate routing information between them. The goal of the project was to enable dynamic routing and facilitate seamless communication between sites, thus eliminating the need for manual static routing.

**Technologies Used**:
- **Dynamic Routing Protocol**: EIGRP (Enhanced Interior Gateway Routing Protocol)
- **Subnetting**: VLSM (Variable Length Subnet Masking)
- **Network Services**: DHCP (Dynamic Host Configuration Protocol), DNS (simulated)
- **Tools**: Cisco Packet Tracer, Cisco IOS

**Key Challenges & Solutions**:
- **Challenge**: Ensuring that routing protocol correctly advertised subnet routes to both sites.
  - **Solution**: Proper EIGRP configuration, including the assignment of an Autonomous System (AS) number and ensuring no automatic summarization of subnets using no auto-summary.
- **Challenge**: Ensuring both sites could assign IPs dynamically to devices without IP conflicts.
  - **Solution**: Implemented a DHCP server on the New York router (R2) and configured static IPs on San Francisco devices, ensuring all IP assignments were correctly allocated.
- **Challenge**: Verifying that both sites could reach each other after EIGRP was configured.
  - **Solution**: Ran connectivity tests (ping) from both sites and validated EIGRP route propagation using routing table commands and neighbor relationships.

[Back to Top](#top)

---

## 4) [Wireshark Network Analysis](https://github.com/caxylive/Net_Projects/tree/main/projects/004%20-%20Wireshark%20Network%20Analysis/README.md)
This project will delve into the practical application of Wireshark for network traffic analysis. Wireshark is a powerful tool used to capture and analyze network packets in real-time, providing invaluable insights into network behavior, troubleshooting issues, and enhancing security.

The focus will be on learning to capture, filter, and interpret network traffic to understand protocol interactions, identify anomalies, and diagnose network problems. This project will cover various aspects of network analysis, including:

  - **Packet Capture**: Setting up Wireshark to capture network traffic on different interfaces.
  - **Filtering**: Using Wireshark's filtering capabilities to isolate specific traffic based on protocols, IP addresses, ports, and other criteria.
  - **Protocol Analysis**: Examining packet details to understand how different protocols (TCP, UDP, IP, HTTP, etc.) function.
  - **Troubleshooting**: Identifying and diagnosing network issues such as latency, packet loss, and connection problems.
  - **Security Analysis**: Detecting suspicious network activity and potential security threats.

**Expected Outcomes**:
  - Proficiency in using Wireshark to capture and analyze network traffic.
  - Ability to interpret packet data and understand protocol behavior.
  - Enhanced troubleshooting skills for diagnosing network issues.
  - Improved understanding of network security concepts through traffic analysis.

**Stay tuned for updates as this project progresses, where I will document the practical steps and findings from my Wireshark analysis sessions.**

[Back to Top](#top)

---
