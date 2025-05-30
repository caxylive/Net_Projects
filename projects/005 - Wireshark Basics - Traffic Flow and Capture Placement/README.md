<a name="top"></a>
[Back to Main](https://github.com/caxylive/Net_Projects/tree/main/README.md)

# Wireshark Basics: Traffic Flow and Capture Placement

---

Author: https://hardworking-lion-z4sd3b.mystrikingly.com/

Contact: carl.xymon.verdejo@gmail.com

---

## Objective

This document focuses on the importance of capture placement in network traffic analysis. The screenshots, diagrams, and the document as a whole demonstrates how traffic flow and switch behavior affect Wireshark captures, highlighting the need for strategic capture points.

---

## Scenario

The same GNS3 topology from [Project 004](https://github.com/caxylive/Net_Projects/tree/main/projects/004%20-%20Wireshark%20Basics%20-%20Analyzing%20HTTP%20Traffic/README.md) is used, consisting of a PC (10.1.1.1), a server (10.1.1.100), and a router (10.1.1.254) acting as a DNS and DHCP server, all connected via a layer 2 switch. The objective is to understand why capturing traffic at certain points in the network does not reveal all communication.

![Network Topology Overview](screenshot/topology.png)

[Back to Top](#top)

---

## Analysis and Observations

1.  **Capture Placement Impact:**
    * Links:
       * Link [1] - between switch and PC
       * Link [2] - between switch and server
       * Link [3] - between switch and router
    * Capturing traffic on Link [3] (rather than on Link [1] or Link [2]) failed to capture HTTP traffic between PC1 and the server.
    * This demonstrates that traffic is not flooded to all ports on a switch once the switch has learned the MAC addresses involved in the communication.
3.  **DNS Traffic Capture:**
    * DNS queries from the PC to the router (DNS server) were captured successfully.
    ![DNS Queries from PC to Router](screenshot/dns-query-pc-to-router.png)
    * This confirmed that the PC was using the router as its DNS server. 
    * The capture showed the DNS query and response, including the resolution of `gns3.com` to 10.1.1.100.
    * The use of UDP port 53 for DNS was observed which is a well known port for DNS. Please note that Port 55037 is an Ephemeral Port and will only last for that session.
    ![DNS Response from Router to PC](screenshot/dns-response-router-to-pc.png)

4.  **Switch MAC Address Table:**
    * The switch's MAC address table was examined to demonstrate how the switch learns and forwards traffic.
    * The switch learned the MAC addresses of the PC, server, and router on their respective ports.
    ![Switch MAC Address Table](screenshot/switch-mac-address-table.png)
    * Once the switch learned the MAC addresses of the PC and server, traffic was forwarded directly between them, not to other ports.
    * After appying an HTTP filter, the screenshot below shows that no HTTP traffic was captured in Link [3].
    ![No HTTP Traffic Captured](screenshot/no-http-traffic-captured.png)
5.  **Traffic Flow Explanation: Switches Learn and Forward**
    * When a device sends traffic to a switch, the switch records the device's MAC address and the port it came from in its MAC address table.
    * Once the switch knows the MAC addresses of both the source and destination devices involved in a conversation, it forwards traffic directly between those two ports.
    * The switch no longer floods the traffic out of all its other ports. This targeted forwarding is how switches improve network efficiency.
    * Therefore, if you want to capture the traffic between two specific devices connected to a switch, you must capture it on the link directly between those devices, or use techniques like port mirroring/spanning or network taps to redirect the traffic to your capture device.
    * Capturing traffic on a link that is not directly in the path of the conversation (i.e., Link [3]) will not show the traffic.
    * This means that in Link [3], although DNS traffic was captured, **no HTTP traffic will be captured**. 
    * Traffic between PC1 and server was directly switched, and did not traverse Link [3].
6.  **Router as DNS/DHCP Server:**
    * The router was configured as a DNS server using `ip dns server`.
    * Static DNS entries were configured to resolve `gns3.com` to 10.1.1.100.
    * The router also acted as a DHCP server, dynamically allocating IP addresses to the PCs.
    * The configuration of the router was shown with `show run | include dns`, and `show interface gigabit 0/0` to show the IP and MAC address of the interface.
    * For configuring routers to act as DNS and DHCP servers (for testing purpose), please refer to [Project 003](https://github.com/caxylive/Net_Projects/blob/main/projects/003%20-%20Inter-Site%20Connectivity%20Using%20EIGRP%20in%20a%20Subnetted%20Network/README.md).

[Back to Top](#top)

---

## Key Takeaways

* **Capture Placement Matters:** The location of the Wireshark capture is critical for capturing specific traffic flows.
* **Switch Behavior:** Switches learn MAC addresses and forward traffic directly between known devices, not flooding to all ports.
* **DNS Operation:** DNS resolves domain names to IP addresses using UDP port 53.
* **Router Functionality:** Cisco routers can act as DNS and DHCP servers.
* **Need for Mirroring/Taps:** To capture traffic between specific devices connected to a switch, port mirroring/spanning or network taps are necessary.

[Back to Top](#top)

---

## Technical Skills Reinforced

* Understanding switch MAC address table behavior.
* Analyzing DNS traffic using Wireshark.
* Understanding the role of a router as a DNS and DHCP server.
* Recognizing the importance of capture placement in network analysis.

---

## Conclusion

This video emphasized the importance of understanding network traffic flow and switch behavior when using Wireshark. It highlighted the need for strategic capture points and the limitations of capturing traffic at arbitrary locations. The next video will demonstrate how to use port mirroring to capture traffic between specific devices.

[Back to Top](#top)

---
