# VLAN Configuration Guide

## Introduction
This document provides a step-by-step guide on how to configure VLANs on a network switch. VLANs help in network segmentation, improving security and efficiency.

## Prerequisites
- A managed switch that supports VLANs
- Basic understanding of networking concepts
- Console or SSH access to the switch

## VLAN Configuration Steps

### 1. Access the Switch
Connect to the switch using:
- **Console cable** (via terminal emulator)
- **SSH** (for remote access)

### 2. Enter Configuration Mode
For Cisco switches:
```
enable
configure terminal
```

### 3. Create VLANs
To create VLANs and assign names:
```
vlan 10
name Sales
exit
vlan 20
name IT
exit
```

### 4. Assign VLANs to Ports
Assign ports to specific VLANs:
```
interface FastEthernet0/1
switchport mode access
switchport access vlan 10
exit

interface FastEthernet0/2
switchport mode access
switchport access vlan 20
exit
```

### 5. Configure Trunk Ports
Trunk ports allow multiple VLANs to pass traffic.
```
interface GigabitEthernet0/1
switchport mode trunk
switchport trunk allowed vlan 10,20
exit
```

### 6. Verify Configuration
Check VLAN assignments:
```
show vlan brief
```
Verify trunk configuration:
```
show interfaces trunk
```

### 7. Save Configuration
Ensure the changes persist after a reboot:
```
write memory
```

## Conclusion
This guide outlines the basic VLAN configuration steps for a managed switch. Proper VLAN implementation enhances network segmentation, security, and efficiency. For further details, consult the official switch documentation or vendor-specific guides.

