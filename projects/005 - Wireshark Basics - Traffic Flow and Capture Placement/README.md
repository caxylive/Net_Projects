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

The same GNS3 topology from the previous video is used, consisting of a PC (10.1.1.1), a server (10.1.1.100), and a router (10.1.1.254) acting as a DNS and DHCP server, all connected via a layer 2 switch. The objective is to understand why capturing traffic at certain points in the network does not reveal all communication.

[Network Topology Overview](screenshot/topology.png)

[Back to Top](#top)

---

## Analysis and Observations

1.  **Capture Placement Impact:**
    * Capturing traffic on the link between the switch and the router (rather than between the switch and PC or switch and server) failed to capture HTTP traffic between the PC and server.
    * This demonstrates that traffic is not flooded to all ports on a switch once the switch has learned the MAC addresses involved in the communication.
2.  **DNS Traffic Capture:**
    * DNS queries from the PC to the router (DNS server) were captured successfully.
    * This confirmed that the PC was using the router as its DNS server.
    * The capture showed the DNS query and response, including the resolution of `gns3.com` to 10.1.1.100.
    * The use of UDP port 53 for DNS was observed.
3.  **Switch MAC Address Table:**
    * The switch's MAC address table was examined to demonstrate how the switch learns and forwards traffic.
    * The switch learned the MAC addresses of the PC, server, and router on their respective ports.
    * Once the switch learned the MAC addresses of the PC and server, traffic was forwarded directly between them, not to other ports.
4.  **Traffic Flow Explanation:**
    * The switch's behavior of forwarding traffic directly between known MAC addresses was explained.
    * This explained why HTTP traffic between the PC and server was not captured on the link between the switch and router.
    * Traffic between the PC and server was directly switched, and did not traverse the link between the switch and the router.
5.  **Router as DNS/DHCP Server:**
    * The router was configured as a DNS server using `ip dns server`.
    * Static DNS entries were configured to resolve `gns3.com` to 10.1.1.100.
    * The router also acted as a DHCP server, dynamically allocating IP addresses to the PCs.
    * The configuration of the router was shown with `show run | include dns`, and `show interface gigabit 0/0` to show the IP and MAC address of the interface.

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
