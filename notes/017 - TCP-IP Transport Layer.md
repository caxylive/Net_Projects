# TCP/IP Transport Layer (Layer 4)

This lesson delves into the TCP/IP transport layer, or layer 4 of the OSI model, focusing specifically on the TCP and UDP protocols.

## 1. Comparison of UDP and TCP

### UDP (User Datagram Protocol)

* **Connectionless protocol:** Does not guarantee packet delivery.
* **Speed over reliability:** Suitable for applications requiring speed.
* **Analogy:** Regular mail (sent without confirmation of delivery).

### TCP (Transmission Control Protocol)

* **Connection-oriented protocol:** Guarantees packet delivery.
* **Reliable data transmission:** Suitable for applications requiring reliability.
* **Analogy:** Telephone call (involves connection setup and acknowledgment).

## 2. Importance of Port Numbers

* Used to identify specific applications and services on a host.
* **Example:** Port 80 for HTTP.

## 3. Mechanisms of TCP

* **TCP Three-Way Handshake:** Ensures a reliable connection is established before data transmission.
* **Windowing:** Manages the flow of data and controls congestion.
* **Sequence Numbers:** Ensures data is received in the correct order and without errors.

## 4. IP Protocol Characteristics

* **Connectionless:** Each packet is treated independently, can take different paths to the destination.
* **No Delivery Guarantee:** Higher layer protocols (like TCP) handle packet reordering and error checking.

## 5. Practical Examples

* **UDP Example:** Data sent without confirmation, suitable for streaming.
* **TCP Example:** Reliable data transmission with acknowledgment, suitable for web browsing.

## 6. Explanation of Sockets

* A combination of an IP address and a port number, used to identify specific applications on a host.

## 7. Session Multiplexing

* Allows a single host with one IP address to communicate with multiple servers and devices simultaneously.

## Useful Commands

| Description of command                    | Command                                                                                                      |
| :------------------------------------------ | :----------------------------------------------------------------------------------------------------------- |
| Show IP Interface Brief                     | `show ip interface brief`                                                                                    |
| Creating a Loopback Interface               | `interface loopback [number]` <br> `ip address [ip-address] [subnet-mask]`                                  |
| Telnet Command                              | `telnet [ip-address]`                                                                                        |
| Enable EIGRP                                | `router eigrp [asn]` <br> `network [network-address] [wildcard-mask]`                                        |
| Enable OSPF                                 | `router ospf [process-id]` <br> `network [network-address] area [area-id]`                                    |
| Show OSPF Interface Brief                   | `show ip ospf interface brief`                                                                               |
| Show OSPF Neighbors                         | `show ip ospf neighbors`                                                                                     |
| Show IP Route                               | `show ip route`                                                                                              |
| Change Line VTY Transport Input             | `line vty 0 4` <br> `transport input all`                                                                    |
| Ping Command                                | `ping [ip-address]`                                                                                          |
| Clear OSPF Processes                        | `clear ip ospf process`                                                                                      |

This lesson covers the key differences between TCP and UDP, the importance of port numbers, and the mechanisms that ensure reliable data transmission in TCP. Understanding these protocols and their functionalities is crucial for network management and troubleshooting.
