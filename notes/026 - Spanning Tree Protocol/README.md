# STP Fundamentals and Root Selection

## 1. **The Importance of Spanning Tree Protocol (STP)**
- Purpose : STP (IEEE 8.2.1D) is a Layer-2 protocol designed to prevent loops in Ethernet networks that use redundant paths for fault tolerance.
- The Problem (without STP): Redundant physical links create a loop, causing brodcast storms (frames loop endlessly), MAC address table instability (port flapping, and network collapse.
- STP Solution : STP creates a single, logical, loop-free path by logically blocking reduntant physical links.

- # 2. **Root Bidge Election (The Global Decision)**

The **Root Bridge (RB)** is the switch at the center of the STP domain, determined by an election process.

- **Criteria:** The switch with the **Lowest Bridge ID (BID)** wins the election.
- **Bridge ID Structure (8 bytes):**
  - Priority (2 Bytes) : Consists of a 4-bit priority field and a 12-bit **Extended System ID** (VLAN ID). The default value is **32768**.
  - MAC Addre`ss (6 bytes): Used as the definitive tie-breaker if priorities are equal.
- Manual Configuration: To force a switch to become the root, its priority must be lowered. The Cisco command `spanning-tree vlan [VLAN ID] root primary` automatically sets a low, winning priority.

- # 3. **Path Cost and Root Port Election**

The **Root Port (RP)** is the port on a non-root switch that provides the best path back to the RB.

- **Path Cost Definition**: The total accumulated cost to travel from a non-root switch back to the Root Bridge. It is the sum of all Port Costs along the path.
- **IEEE Port Costs (Default Cisco/1998):** The cost is inversely proportional to the link speed.
  - 100 Mbps (Fast Ethernet): 19
  - **1 Gbps (Gigabit Ethernet): 4**
  - 10 Gbps: 2
- **Root Port (RP) Criteria (Tie-breakers in order):** The RP is chosen based on the superior BPDU received:
  1. **Lowest Path Cost** (Best path back to the root).
  2. **Lowest Neighbor Bridge ID**
  3. **Lowest Port Priority** (Default 128)
  4. **Lowest Port ID** (e.g., Gig 0/0 is lower than Gig 0/1) 
