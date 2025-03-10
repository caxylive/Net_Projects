<a name="top"></a>
[Back to Main](https://github.com/caxylive/Net_Projects/tree/main/notes)

# TCP Window Sizes and Their Impact

## Basic TCP Window Size
- **Window Size = 1**: Each segment sent by the sender requires an acknowledgement (ACK) before sending the next segment. This leads to low throughput.

[Back to Top](#top)

---

## Increasing Window Size
- **Larger Window Sizes**: More segments can be transmitted before receiving an ACK. This improves throughput and efficiency.

[Back to Top](#top)

---

## Fixed Window Size Example
- **Window Size = 3**:
  - Host A sends segments 1, 2, and 3 to Host B.
  - Host B acknowledges for segment 4.
  - Host A sends the next segments 4, 5, and 6.
  - Host B acknowledges for segment 7, and the process continues.

[Back to Top](#top)

---

## Sliding Window
- **Dynamic Adjustment**: The window size changes based on network conditions and receiver capacity.
  - If a packet is dropped, the window size decreases to prevent congestion.
  - Example: Window size starts at 5, increases to 7, then to 10 based on successful transmissions and network handling.

[Back to Top](#top)

---

## Congestion Control
- **Congestion Window (CWND)**: Controls the amount of data sent. Starts small and increases exponentially until a packet loss occurs.
- **Packet Loss**: When a packet is lost, the congestion window size is halved and then gradually increased again.
- **Congestion Avoidance**: Algorithm used to slow down growth of the window size to prevent further losses.

[Back to Top](#top)

---

## Quality of Service (WRED)
- **Weighted Random Early Detection**: Technique to improve efficiency by randomly dropping packets from various flows to prevent global synchronization.
- **Global Synchronization**: Multiple hosts slow down and speed up simultaneously, leading to inefficiency.

[Back to Top](#top)

---

# Key Concepts
- **Window Size**: The number of segments the sender can send before needing an acknowledgement.
- **Acknowledgement (ACK)**: The receiver sends an ACK for the next expected segment.
- **Sliding Window**: Dynamic adjustment of the window size to optimize data transmission.
- **Congestion Window (CWND)**: Manages network congestion by controlling the amount of data sent.
- **Quality of Service (WRED)**: Improves TCP efficiency by preventing global synchronization.

[Back to Top](#top)

---

# Examples

## Small Window Size
- **Window Size = 2**:
  - Host A sends segments 1 and 2.
  - Host B acknowledges for segment 3, and the process continues.

[Back to Top](#top)

---

## Large Window Size
- **Window Size = 10**:
  - Host A sends segments 1 to 10.
  - Host B acknowledges for segment 11, and so on.

[Back to Top](#top)

---

## Packet Loss and Congestion Control
- **Initial CWND = 4**:
  - Host A sends segments 1 to 4.
  - Segment 3 is lost, Host B acknowledges for segment 2.
  - Host A retransmits segment 3 and reduces the window size to prevent further congestion.

[Back to Top](#top)

---
