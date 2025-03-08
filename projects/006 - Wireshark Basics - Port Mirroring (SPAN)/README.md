# Wireshark Basics: Port Mirroring (SPAN) (David Bombal - Part 3)

## Objective

This document summarizes David Bombal's "Wireshark Basics - Part 3" video, which demonstrates how to use port mirroring (SPAN) to capture traffic between specific devices in a switched network. The video highlights the limitations of capturing traffic at arbitrary locations and the necessity of port mirroring for comprehensive network analysis.

## Scenario

The GNS3 topology from the previous videos is used. An Ubuntu PC is added to the topology to simulate a monitoring station. The goal is to capture HTTP traffic between the PC and server by using port mirroring.

## Analysis and Observations

1.  **Initial Capture Failure:**
    * Capturing traffic on the link between the switch and the router (as done in the previous video) still fails to capture HTTP traffic between the PC and server.
    * This reinforces the concept that switches do not flood traffic to all ports once MAC addresses are learned.
2.  **Port Mirroring (SPAN) Configuration:**
    * Port mirroring (SPAN) is configured on the switch to copy traffic from the PC-switch link to the Ubuntu PC link.
    * The following commands are used:
        * `monitor session 1 source interface gigabit 0/0`
        * `monitor session 1 destination interface gigabit 0/3`
    * This configuration copies all traffic from gigabit 0/0 (PC-switch link) to gigabit 0/3 (Ubuntu PC link).
3.  **Successful HTTP Traffic Capture:**
    * After configuring port mirroring, HTTP traffic between the PC and server is successfully captured on the Ubuntu PC link.
    * This demonstrates the effectiveness of port mirroring for capturing traffic between specific devices.
4.  **Verification of SPAN Configuration:**
    * The `show monitor session 1` command is used to verify the SPAN configuration.
    * This command displays the source and destination interfaces, as well as the encapsulation type.
5.  **HTTP Traffic Analysis:**
    * The captured HTTP traffic is analyzed in Wireshark.
    * The source and destination MAC addresses, IP addresses, and port numbers are examined.
    * The HTTP requests and responses, including the HTML content and PNG file, are observed.
    * The concept of the browser caching data is shown, and how a private browsing session can force new requests.
6.  **Importance of Capture Placement:**
    * The video reiterates the importance of capture placement and the limitations of capturing traffic at arbitrary locations.
    * The necessity of using port mirroring or other techniques to capture traffic between specific devices is emphasized.
6.  **Remote SPAN and Overhead:**
    * The video mentions remote SPAN, which allows copying traffic through a tunnel to a remote monitoring station.
    * The potential overhead and traffic volume associated with remote SPAN are discussed.
    * Capturing traffic locally is recommended whenever possible.

## Key Takeaways

* **Port Mirroring (SPAN):** Port mirroring allows copying traffic from one or more interfaces to a destination interface for monitoring purposes.
* **Capture Placement:** The location of the Wireshark capture is critical for capturing specific traffic flows.
* **Switch Behavior:** Switches forward traffic directly between known MAC addresses, not flooding to all ports.
* **Monitoring Station:** Port mirroring allows a monitoring station to capture traffic between specific devices.
* **Remote SPAN:** Remote SPAN allows capturing remote traffic, but it adds overhead.

## Technical Skills Reinforced

* Configuring port mirroring (SPAN) on a Cisco switch.
* Verifying SPAN configuration.
* Analyzing captured HTTP traffic in Wireshark.
* Understanding the importance of capture placement.
* Understanding the role of a monitoring station.

## Conclusion

This video demonstrated the practical application of port mirroring for capturing traffic between specific devices in a switched network. It reinforced the importance of capture placement and highlighted the limitations of capturing traffic at arbitrary locations. Port mirroring is a valuable tool for network analysis and troubleshooting.
