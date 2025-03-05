# TCP/IP Transport Layer (Layer 4): TCP & UDP

This lesson explores the TCP/IP transport layer, focusing on TCP and UDP protocols, data segmentation, flow control, and protocol comparison.

## 1. Comparison of UDP and TCP

### UDP (User Datagram Protocol)

* **Connectionless:** Does not guarantee packet delivery.
* **Speed over reliability:** Suitable for applications requiring speed.
* **Analogy:** Regular mail (sent without confirmation of delivery).
* **Applications:** VoIP, video streaming.

### TCP (Transmission Control Protocol)

* **Connection-oriented:** Guarantees packet delivery.
* **Reliable data transmission:** Suitable for applications requiring reliability.
* **Analogy:** Telephone call (involves connection setup and acknowledgment).
* **Applications:** HTTP, email, FTP, file transfer (FTP, TFTP, NFS), remote login (Telnet, SSH), network management (SNMP), name management (DNS).
* **Full Duplex:** Allows simultaneous transmission and reception of data.

| Feature             | TCP                                      | UDP                                      |
| :------------------ | :--------------------------------------- | :--------------------------------------- |
| Connection          | Connection-oriented (three-way handshake) | Connectionless                           |
| Reliability         | Reliable (ACKs, sequence numbers)        | Unreliable (best-effort)                 |
| Sequence Numbers    | Yes                                      | No                                       |
| Retransmissions     | Yes                                      | No                                       |
| Flow Control        | Yes (sliding window)                     | No (relies on higher-layer protocols)   |
| Error Checking      | Checksums                                | Optional Checksums(Mandatory in IPv6)   |

## 2. Importance of Port Numbers

* Used to identify specific applications and services on a host.
* **Example:** Port 80 for HTTP.

## 3. Mechanisms of TCP

* **TCP Three-Way Handshake:** Establishes a reliable connection.
* **Windowing:** Manages data flow and congestion.
* **Sequence Numbers:** Ensures data is received in order and without errors.
* **Acknowledgements:** Receiver acknowledges receipt of data, enabling re-transmission.
* **Data Recovery:** Re-transmits lost segments.

## 4. IP Protocol Characteristics

* **Connectionless:** Packets treated independently, can take different paths.
* **No Delivery Guarantee:** Higher layer protocols handle reordering and error checking.

## 5. Data Segmentation and MTU/MSS

* **Segmentation:** Data broken into smaller chunks for transmission.
* **Maximum Transmission Unit (MTU):** Largest packet size an interface can handle (e.g., 1,500 bytes for Fast Ethernet).
* **TCP Packet Size:** Theoretically, up to 65,495 bytes.
* **Fragmentation:** Breaking large packets into smaller ones when exceeding MTU.
* **Maximum Segment Size (MSS):** Largest data amount TCP sends in a single segment (avoid fragmentation).
* **Path MTU Discovery:**
    * Determines the smallest MTU along the path.
    * Avoids fragmentation.
    * Optional in IPv4, mandatory in IPv6.
    * IPv6 does not support router fragmentation.
* **UDP and Fragmentation:** UDP relies on higher-layer protocols for fragmentation.

## 6. Flow Control

* **Purpose:** Prevents sender from overwhelming receiver.
* **TCP Flow Control:**
    * Uses acknowledgments (ACKs) and sliding window.
    * Receiver advertises receive window.
* **UDP Flow Control:**
    * Not implemented.
    * Higher-layer protocols handle flow control.

## 7. Explanation of Sockets

* Combination of IP address and port number.

## 8. Session Multiplexing

* Allows a single host to communicate with multiple servers simultaneously.

## 9. UDP Deep Dive

* **Transport Layer Protocol:** OSI layer 4.
* **Access to Network Layer:** Without reliability overhead.
* **Connectionless:** Sends datagrams without setup.
* **Limited Error Checking:**
    * Optional checksum (mandatory in IPv6).
    * Destination port unreachable messages.
* **Best-Effort Delivery:**
    * No delivery guarantee.
    * Higher-layer protocols handle reliability.
* **No Data Recovery:** Higher-layer protocols handle recovery.
* **TFTP Example:** Uses UDP but implements its own reliability.

### UDP Header

* **Source Port:** 16-bit.
* **Destination Port:** 16-bit.
* **UDP Length:** 16-bit (header + data).
    * Minimum: 8 bytes.
    * Maximum: 65,535 bytes (IPv4: 65,507 bytes).
* **UDP Checksum:** 16-bit (optional in IPv4, mandatory in IPv6).

## 10. TCP Header

* **Source Port:** 16-bit identifier for the sending port.
* **Destination Port:** 16-bit identifier for the receiving port.
* **Sequence Number:** 32-bit number for segment ordering.
* **Acknowledgement Number:** 32-bit number for acknowledging received data.
* **Header Length:** Specifies the size of the TCP header.
* **Flags:** Various control flags (URG, ACK, PSH, RST, SYN, FIN).
* **Window Size:** 16-bit field for flow control.
* **Checksum:** 16-bit field for error checking.
* **Urgent Pointer:** Indicates the end of urgent data.
* **Options:** Various additional options for TCP.

## 11. OSI Model Layer Mapping

* **Layer 2 (Data Link):** Uses type numbers to differentiate multiple layer 3 protocols.
* **Layer 3 (Network):** Uses protocol numbers to differentiate layer 4 protocols (TCP, UDP).
* **Layer 4 (Transport):** Uses port numbers to differentiate multiple applications at layer 7.

## 12. Practical Examples

* **Duplex and Speed Mismatch:** Issues caused by auto-negotiation failures or manual mismatches.
* **Full-Duplex vs. Half-Duplex:** Differences in transmission methods and potential errors to look for.

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
