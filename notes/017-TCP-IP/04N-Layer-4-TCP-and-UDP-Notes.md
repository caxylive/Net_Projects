<a name="top"></a>
[Back to Main](https://github.com/caxylive/Net_Projects/tree/main/notes)

# Layer 4: TCP & UDP Notes

## Layer 4 Overview: Transport Layer

* Deals with end-to-end communication.
* Key protocols: TCP and UDP.
* Uses port numbers to identify applications.

## Port Numbers

* **Source Port:** Port used by the sending application.
* **Destination Port:** Port used by the receiving application.
* **Well-Known Ports:** 0-1023 (e.g., 80 for HTTP, 23 for Telnet, 53 for DNS).
* **Ephemeral Ports:** 1024-65535 (dynamically assigned).
* **Port Reversal:** Source and destination ports are swapped in reply traffic.

```
+----------------+       +----------------+
| Host A (1024)  |------>| Host B (23)    |
| (Source Port)  |       | (Dest Port)    |
+----------------+       +----------------+
        ^                 |
        |-----------------|
        |                 v
+----------------+       +----------------+
| Host A (1024)  |<------| Host B (23)    |
| (Dest Port)    |       | (Source Port)  |
+----------------+       +----------------+
```

## UDP (User Datagram Protocol)

* **Connectionless:** No handshake, less reliable.
* **Fast:** Lower overhead.
* **Use Cases:** DNS, streaming, VoIP.
* Protocol number: 17.

## TCP (Transmission Control Protocol)

* **Connection-Oriented:** Requires a handshake, reliable.
* **Slower:** Higher overhead due to reliability features.
* **Use Cases:** Web browsing, file transfer.
* Protocol number: 6.

### TCP Three-Way Handshake

```
Host A (Client)          Host B (Server)

    SYN (Seq=X)   --------->
                   <---------   SYN-ACK (Seq=Y, Ack=X+1)
    ACK (Ack=Y+1) --------->
```

* **SYN:** Synchronize sequence numbers.
* **SYN-ACK:** Synchronize and acknowledge.
* **ACK:** Acknowledge.

### TCP Sequence and Acknowledgement Numbers

* **Sequence Number:** Tracks the order of data segments.
* **Acknowledgement Number:** Indicates the next expected sequence number.
* Ensures reliable delivery and reassembly of data.

### TCP Windowing

* Allows multiple data segments to be sent before acknowledgement.
* Improves efficiency.
* Window size is measured in bytes.
* **MSS (Maximum Segment Size):** Limits the size of each TCP segment.

## Wireshark Analysis

* Tool for capturing and analyzing network traffic.
* Shows Layer 2, 3, and 4 details.
* Helps visualize TCP/UDP behavior.

### Example: DNS (UDP)

* Source Port: Ephemeral (e.g., 62249).
* Destination Port: 53.
* Shows DNS queries and responses.

### Example: HTTP (TCP)

* Three-way handshake (SYN, SYN-ACK, ACK).
* Data transfer with sequence and acknowledgement numbers.
* Port 80 (HTTP).
* TCP flags: SYN, ACK, FIN, RST, PSH, URG.
* TCP Segment reassembly.

## Key Concepts

* **Reliability:** TCP provides reliability, UDP does not.
* **Connection:** TCP is connection-oriented, UDP is connectionless.
* **Efficiency:** UDP is more efficient for real-time applications.
* **Port Numbers:** Essential for identifying applications.
* **Wireshark:** Essential for network analysis.
