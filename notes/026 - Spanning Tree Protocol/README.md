# STP Fundamentals and Root Selection

## 1. **The Importance of Spanning Tree Protocol (STP)**
- Purpose : STP (IEEE 8.2.1D) is a Layer-2 protocol designed to prevent loops in Ethernet networks that use redundant paths for fault tolerance.
- The Problem (without STP): Redundant physical links create a loop, causing brodcast storms (frames loop endlessly), MAC address table instability (port flapping, and network collapse.
- STP Solution : STP creates a single, logical, loop-free path by logically blocking reduntant physical links.

## 2. **Root Bridge Election (The Global Decision)**

The **Root Bridge (RB)** is the switch at the center of the STP domain, determined by an election process.

- **Criteria:** The switch with the **Lowest Bridge ID (BID)** wins the election.
- **Bridge ID Structure (8 bytes):**
  - Priority (2 Bytes) : Consists of a 4-bit priority field and a 12-bit **Extended System ID** (VLAN ID). The default value is **32768**.
  - MAC Addre`ss (6 bytes): Used as the definitive tie-breaker if priorities are equal.
- Manual Configuration: To force a switch to become the root, its priority must be lowered. The Cisco command `spanning-tree vlan [VLAN ID] root primary` automatically sets a low, winning priority.

## 3. **Path Cost and Root Port Election**

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

---

# RSTP and Port Role Enhancements

## 1. Traditional STP (802.1D / PVST) Convergence

This standard uses passive, timer-based convergence, leadingosignificant delays.
- Mechanism: Relies on fixed timers to transition ports through states.
  - Max Age (20s) : Blocking --> Listening
  - Forward Delay (15s) : Listening --> Learning
  - Forward Delay (15s) : Learning --> Forwarding
- Converge Time : Slow (30 - 50 seconds) for link state changes.
- Problem: Causes network outages and application timeouts (e.g. DHCP failure) during link failure or recovery.

## 2. Rapid STP (802.1W / Rapid PVST+) Convergence

RSTP achieves rapid convergence by using an active, timer-independent mechanism.

- **Mechanism:** Uses an **active bridge-to-bridge handshake** instead of timers, allowing ports to move immediately to the Forwarding state.

- **Convergence Time: Fast** (sub-second).

- **Backward Compatibility**: R-PVST+ is compatible with 802.1D, but negotiation falls back to the **slow 802.1D timers** on the connecting link.

## 3. RSTP Port States and Roles

RSTP consolidates old states and introduces new roles for greater efficiency in managing blocked ports.

| 802.1D State	                | RSTP (802.1w) State	| Notes                                                     |
|-------------------------------|---------------------|-----------------------------------------------------------|
| Disabled, Blocking, Listening	| Discarding	        | Unified blocking/disabled state.                          |
| Learning	                    | Learning	          | Updates MAC table, but does not forward user traffic.     |
| Forwarding	                  | Forwarding	        | Fully operational; forwards user traffic and learns MACs. |

| RSTP Role	          | Corresponds to 802.1D	| Function/Reason for Blocking                                                                 |
|---------------------|-----------------------|----------------------------------------------------------------------------------------------|
| Alternate Port (AP)	| Blocking	            | Offers an alternate path to the Root via a different switch. Ready for immediate transition. |
| Backup Port (BP)	  | Blocking	            | Offers a redundant connection to the same segment on the same switch (e.g., via a hub).      |

## 4. Dynamic Re-Convergence Demonstration

- **RSTP Speed**: When the **Root Port** fails, the **Alternate Port** immediately transitions to Forwarding in sub-second time via the handshake mechanism (on point-to-point links).

- **PVST Speed**: When the Root Port fails, the alternate path must wait through the Listening and Learning phases (30 seconds) before it can forward traffic.

---

# RSTP Fast Convergence Mechanisms

## 1. **The Core Difference: Active vs. Passive Convergence**

**Legacy STP (802.1D): Passive**. It waited for the network to converge based on fixed, conservative timers (Forward Delay=15s, Max Age=20s).

**Rapid STP (802.1w): Active**. It uses an **active negotiation/handshake mechanism** to confirm the safety of a path, allowing the port to transition to **Forwarding immediately**, without relying on the 802.1D timers.

## 2. **Proposal / Agreement Handshake (Point-to-Point Links)**

This is the primary mechanism for sub-second convergence on links between switches.

- **Requirement:** This sequence works effectively only on **Point-to-Point links** (typically full-duplex).

- **Trigger:** Initiated when a port comes up or when a non-Root Switch receives a **superior BPDU** (better path) from a neighbor.

- **BPDU Enhancements:** RSTP BPDUs contain specific fields (like the **Proposal** and **Agreement** bits) to facilitate the handshake.

- **Sequence**:

  1. **Proposal Sent**: The designated switch (e.g., the Root) sends a BPDU with the **Proposal bit set**.

  2. **Synchronization (Sync)**: The receiving switch (Switch A) selects the port as its new **Root Port (RP)**. Switch A immediately forces all other **non-Edge ports** into the **Discarding** state (Syncing).

  3. **Agreement Sent**: Once synchronization is complete, Switch A immediately transitions the new RP to **Forwarding** and sends an **Agreement** message back.

  4. **Instant Forwarding**: The Designated Port on the neighbor receives the Agreement and immediately transitions to **Forwarding**.

 ## 3. **Edge Ports (PortFast)**

Edge ports eliminate convergence delay for end-devices.

**Function:** Immediately transitions the port to the **Forwarding** state, skipping the Listening and Learning phases.

**Use Case:** Must **only** be used on access ports connected to end-user devices (PCs, servers, routers), **never** on inter-switch links.

**Topology Changes:** Edge Ports **do not generate TCNs** (Topology Change Notifications) when the link state toggles, which prevents unnecessary network recalculations.

**Security Feature:** An Edge Port that unexpectedly **receives a BPDU** immediately **loses its Edge Port status** and reverts to a normal STP port, preventing accidental loops if a switch is plugged in.

**Cisco Command:** `spanning-tree portfast` is used to configure an Edge Port.

---

## 4. **Link Type and Fallback**

The switch determines its convergence behavior based on the link type.

**Point-to-Point:** Assumed on **full-duplex** links. Allows the **rapid handshake**.

**Shared Port:** Assumed on **half-duplex** links (e.g., connection to a hub). RSTP **reverts to the slow 802.1D timers** (Listening/Learning sequence) for safety, resulting in a 30-second delay.

**Manual Override:** You can manually configure the link type: `spanning-tree link-type point-to-point`.
