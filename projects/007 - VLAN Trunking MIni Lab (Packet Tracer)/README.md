# VLAN Trunking Mini Lab (Packet Tracer)

## Objective
This lab demonstrates how to configure VLANs, access ports, and trunking between two switches in a small enterprise-style topology. It also shows how to connect routers as end devices (acting as PCs) and assign them to specific VLANs.  

The exercise provides hands-on practice with:  
- VLAN creation and assignment  
- Access port configuration  
- Trunk configuration using 802.1Q  
- Port mapping and IP addressing  

---

## Topology
``` ascii
         +-------------------+
         |       Switch 1    |
         |                   |
R1 (PC A)---+Gi1/0/1 Gi1/0/24+---+Gi1/0/24 Switch 2
VLAN 1 | | | |
R2 (PC B)---+Gi1/0/2 | | Gi1/0/1 +---R3 (PC C)
VLAN 2 +-------------------+ | | VLAN 1
| Gi1/0/2 +---R4 (PC D)
| | VLAN 2
+-------------------+
```

---

## Port Mapping & IP Addresses

| Device | Interface | Switch Port | VLAN | IP Address   |
|--------|-----------|-------------|------|--------------|
| R1     | G0/0      | S1 Gi1/0/1  | 1    | 10.1.1.1/24  |
| R2     | G0/0      | S1 Gi1/0/2  | 2    | 10.1.2.2/24  |
| R3     | G0/0      | S2 Gi1/0/1  | 1    | 10.1.1.3/24  |
| R4     | G0/0      | S2 Gi1/0/2  | 2    | 10.1.2.4/24  |
| S1     | Gi1/0/24  | ---         | Trunk| ---          |
| S2     | Gi1/0/24  | ---         | Trunk| ---          |

---

## Configuration

### Switch 1 (S1)

``` plaintext
enable
configure terminal

! Configure VLANs
vlan 1
 name VLAN1
vlan 2
 name VLAN2

! Assign ports to VLANs
interface gi1/0/1
 switchport mode access
 switchport access vlan 1
 no shutdown

interface gi1/0/2
 switchport mode access
 switchport access vlan 2
 no shutdown

! Configure trunk link to S2
interface gi1/0/24
 switchport mode trunk
 no shutdown
```

Explanation:
- switchport mode access → forces the port into access mode.
- switchport access vlan X → assigns the port to VLAN X.
- switchport mode trunk → enables trunking (802.1Q by default in Packet Tracer).
- no shutdown → activates the interface.

### Switch 2 (S2)

``` plaintext
enable
configure terminal

! Configure VLANs
vlan 1
 name VLAN1
vlan 2
 name VLAN2

! Assign ports to VLANs
interface gi1/0/1
 switchport mode access
 switchport access vlan 1
 no shutdown

interface gi1/0/2
 switchport mode access
 switchport access vlan 2
 no shutdown

! Configure trunk link to S1
interface gi1/0/24
 switchport mode trunk
 no shutdown
```

### Routers (acting as PCs)
### R1
``` plaintext
enable
configure terminal
interface g0/0
 ip address 10.1.1.1 255.255.255.0
 no shutdown
```

### R2
``` plaintext
enable
configure terminal
interface g0/0
 ip address 10.1.2.2 255.255.255.0
 no shutdown
```

### R3
``` plaintext
enable
configure terminal
interface g0/0
 ip address 10.1.1.3 255.255.255.0
 no shutdown
```

### R4
``` plaintext
enable
configure terminal
interface g0/0
 ip address 10.1.2.4 255.255.255.0
 no shutdown
```

## Verification
### Check VLANs on switches:
``` Cisco IOS
show vlan brief
```

### Check trunk status:
``` Cisco IOS
show interface trunk
```

### Ping tests:
- R1 ↔ R3 (VLAN 1, should succeed)

- R2 ↔ R4 (VLAN 2, should succeed)

- R1 ↔ R2 (different VLANs, should fail unless routed)
