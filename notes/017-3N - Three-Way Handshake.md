<a name="top"></a>
[Back to Main](https://github.com/caxylive/Net_Projects/tree/main/notes)

---

# TCP Connection Establishment and Data Transfer

---

## Connection Establishment (Three-Way Handshake)

* **Connection-Oriented:** TCP requires a connection to be established before data transmission.

```
Host A                                     Host B

   |                                          |
   | SYN, seq=100                             |
   |----------------------------------------->|
   |                                          |
   |                SYN-ACK, seq=300, ack=101 |
   |<-----------------------------------------|
   |                                          |
   | ACK, seq=101, ack=301                    |
   |----------------------------------------->|
   |                                          |
   |--------------------Data Exchange------------------->|
```

* **Three-Way Handshake Process:**
    1.  **SYN (Synchronization):**
        * Host A (initiator) sends a TCP segment to Host B.
        * SYN flag is set (SYN = 1).
        * Host A chooses an initial sequence number (e.g., 100).
        * Specifies the destination port (e.g., 80 for HTTP).
    2.  **SYN-ACK (Synchronization-Acknowledgement):**
        * Host B (receiver) receives the SYN and acknowledges it.
        * SYN and ACK flags are set (SYN = 1, ACK = 1).
        * Host B chooses its own initial sequence number (e.g., 300).
        * Host B sets the acknowledgement number to A's sequence number + 1 (e.g., 101).
    3.  **ACK (Acknowledgement):**
        * Host A receives the SYN-ACK and acknowledges it.
        * ACK flag is set (ACK = 1).
        * Host A sets the acknowledgement number to B's sequence number + 1 (e.g. 301).
        * Host A sends it's sequence number incremented by 1 (e.g. 101)
        * SYN flag is cleared (SYN = 0), indicating the handshake is complete.

[Back to Top](#top)

---

## Sequence Numbers and Acknowledgements

* **Purpose:** Ensure reliable data delivery and proper ordering.
* **Sequence Numbers:**
    * Assigned to each TCP segment.
    * Used to track the order of segments.
    * Initial sequence numbers are randomly chosen and communicated during the handshake.
* **Acknowledgements:**
    * Indicate the next sequence number the receiver expects.
    * Implies that all previous segments have been received successfully.
    * Example: if host B sends an ACK of 6, it means it has received everything up to sequence number 5.
* **Window Size:**
    * Maximum amount of data a receiver can receive and process before acknowledgement.
    * Example: Window size of 1 means only one segment can be sent before an ACK is required.

[Back to Top](#top)

---

## Flow Control

* **Purpose:** Prevent receiver buffer overflow.
* **Mechanism:**
    * Receiver can adjust the window size to control the sender's transmission rate.
    * Setting window size to 0: Tells the sender to stop sending data.
    * Increasing window size: Allows sender to transmit more data before receiving acknowledgements, increasing throughput.
* **Benefits:**
    * Enables communication between devices with different processing capabilities.
    * Optimizes network utilization.
    * Reduces round trip times when window sizes are increased.

[Back to Top](#top)

---
