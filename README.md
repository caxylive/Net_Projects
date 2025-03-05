<a name="top"></a>
# My Networking Projects
This repository serves as a collection of networking projects designed to enhance my technical knowledge and practical skills in IT. Each project focuses on key networking concepts such as subnetting, routing, and network configuration, reinforcing my understanding as I progress in my IT journey.

---
## Table of Contents
|Project Number | Project Title                                                                                                                                   |
|:-------------:|-------------------------------------------------------------------------------------------------------------------------------------------------|
| 001           | [Subnetting, Network Configuration and Management](#1-subnetting-network-configuration-and-management)                                          |
| 002           | [Optimizing Network Subnetting and Configuration for Site Expansion](#2-optimizing-network-subnetting-and-configuration-for-site-expansion)     |
| 003           | [Inter-Site Connectivity Using EIGRP in a Subnetted Network](#3-inter-site-connectivity-using-eigrp-in-a-subnetted-network)                     |
| 004           | [Coming Soon](#4-coming-soon)                                                                                                                   |

---

## 1) [Subnetting, Network Configuration and Management](https://github.com/caxylive/Net_Projects/tree/main/projects/001%20-%20Subnetting%20Network%20Configuration%20and%20Management)
This project focuses on subnetting an allocated network into smaller subnets to accommodate multiple network segments. I configured IP addressing, set up devices for internal communication, and enabled external network access. The goal was to design a scalable and well-organized network that supports efficient IP address allocation, reduces waste, and ensures seamless connectivity within and outside of subnets.

Tools Used:
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

Tools Used:
- Cisco Packet Tracer
- Routers, Switches, VLANs, Routing Protocols (OSPF or EIGRP depending on the setup)

Key Challenges & Solutions:
- Challenge: Managing IP address allocation while expanding the network for an additional site.
- Solution: Carefully planned subnetting to accommodate the new site and integrated it without IP conflicts.
- Challenge: Ensuring the network scales without causing bottlenecks or inefficiencies.
- Solution: Configured routing protocols to facilitate smooth communication between the sites, prioritizing efficiency and redundancy.

[Back to Top](#top)

---

## 3) [Inter-Site Connectivity Using EIGRP in a Subnetted Network](https://github.com/caxylive/Net_Projects/tree/main/projects/003%20-%20Inter-Site%20Connectivity%20Using%20EIGRP%20in%20a%20Subnetted%20Network)
In modern network infrastructures, efficient routing is essential to ensure seamless communication between different sites. This project involves configuring and implementing the Enhanced Interior Gateway Routing Protocol (EIGRP) to enable full network connectivity between two locations: San Francisco and New York. Prior to configuring EIGRP, devices within each site could communicate locally, but inter-site communication was not possible. The goal of this project is to enable dynamic routing using EIGRP so that devices from both sites can reach each other efficiently.

[Back to Top](#top)

---

## 4) Coming Soon!
Stay tuned for more exciting networking projects that explore advanced routing protocols, network security, and real-world network design solutions.

[Back to Top](#top)
