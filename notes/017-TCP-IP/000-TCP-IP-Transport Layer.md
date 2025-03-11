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

| Feature                | TCP                                                              | UDP                                                              |
| :--------------------- | :----------------------------------------------------------------- | :----------------------------------------------------------------- |
| Connection             | Connection-oriented (three-way handshake)                         | Connectionless                                                   |
| Reliability            | Reliable (ACKs, sequence numbers, data recovery)                  | Unreliable (best-effort)                                         |
| Sequence Numbers       | Yes (ensures data order)                                           | No                                                               |
| Retransmissions        | Yes (for lost or corrupted packets)                                | No                                                               |
| Flow Control           | Yes (sliding window)                                               | No (relies on higher-layer protocols)                              |
| Error Checking         | Checksums                                                          | Optional Checksums (Mandatory in IPv6)                             |
| Full Duplex Mode       | Yes (both hosts can transmit and receive simultaneously)           | Not applicable (connectionless)                                  |
| Acknowledgement        | Yes (receipt of data)                                              | No                                                               |
| Data Recovery          | Yes (re-transmits lost segments)                                   | No (relies on higher-layer protocols)                              |

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

```
  0                   1                   2                   3
  0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
 +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
 |      16-bit Source Port        |     16-bit Destination Port  |
 +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
 |                    32-bit Sequence Number                     |
 +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
 |                 32-bit Acknowledgement Number                 |
 +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
 |  Data |           |U|A|P|R|S|F|                               |
 | Offset| Reserved  |R|C|S|S|Y|I|            Window             |
 |       |           |G|K|H|T|N|N|                               |
 +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
 |       16-bit Checksum         |         Urgent Pointer        |
 +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
 |                    Options                    |    Padding    |
 +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
 |                             Data                              |
 +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

* **Source Port (16-bit):**
    * Identifies the sending port.
* **Destination Port (16-bit):**
    * Identifies the receiving port.
* **Sequence Number (32-bit):**
    * If the SYN bit is set, this is the initial sequence number.
    * If the SYN bit is not set, this is the accumulated sequence number of the first data byte of the current session.
* **Acknowledgement Number (32-bit):**
    * If the ACK bit is set, this value is the next sequence number that the receiver expects to receive, acknowledging the receipt of all prior bytes.
* **Header Length/Data Offset:**
    * Specifies the size of the TCP header in 32-bit words.
    * Minimum size: 5 words   ;   20 -bits
    * Maximum size: 15 words  ;   60-bits
* **Reserved:**
    * Set to 0 for future use.
* **Flags/Control Bits:**
    * **URG:** Urgent pointer field significant.
    * **ACK:** Acknowledgment field significant.
    * **PSH:** Push Function.
    * **RST:** Reset the connection.
    * **SYN:** Synchronize sequence numbers.
    * **FIN:** No more data from the sender.
* **Window Size (16-bit):**
    * Specifies the size of the receiver's window, indicating the number of bytes the receiver is willing to receive.
* **Checksum (16-bit):**
    * Used for error-checking the header and data.
* **Urgent Pointer (16-bit):**
    * If the URG flag is set, this value is an offset from the sequence number, indicating the last urgent data byte.
* **Options:**
    * Various options for TCP, out of scope for this course.
* **Data:**
    * Higher layer protocol data encapsulated within the TCP header.

---

### Examples;

1. URG (Urgent pointer field significant)
Example: If an application sends urgent data that needs immediate attention (like an interrupt signal), the URG flag is set. The urgent pointer in the TCP header indicates the end of the urgent data, so the receiving TCP knows to prioritize processing this data first.

2. ACK (Acknowledgment field significant)
Example: When a host receives data and wants to acknowledge the receipt, it sets the ACK flag. For example, when Host A sends data to Host B, Host B will send an acknowledgment (ACK) back to Host A indicating the successful receipt of the data.

3. PSH (Push Function)
Example: If data needs to be sent immediately rather than waiting to fill the TCP buffer, the PSH flag is set. For instance, in an interactive application like a chat program, when a user sends a message, the PSH flag can be set to ensure the data is delivered immediately.

4. RST (Reset the connection)
Example: If a connection needs to be terminated abruptly (e.g., due to an error or unexpected condition), the RST flag is set. If Host A sends data to Host B, but Host B doesn’t recognize the connection (e.g., because it was already closed), Host B will send a TCP segment with the RST flag set to reset the connection.

5. SYN (Synchronize sequence numbers)
Example: The SYN flag is used during the initial handshake process to establish a connection. When Host A wants to start a connection with Host B, it sends a TCP segment with the SYN flag set. Host B responds with a segment that also has the SYN flag set, and an acknowledgment (ACK).

6. FIN (No more data from the sender)
Example: When a host has finished sending data and wants to close the connection, it sets the FIN flag. For example, after Host A has sent all its data to Host B, it sends a segment with the FIN flag set to indicate no more data will be sent, initiating the connection termination process.

These flags play crucial roles in managing and controlling TCP connections to ensure reliable and ordered data transmission. If you have any more questions or need further clarification, feel free to ask!

---

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
