<a name="top"></a>
[Back to Main](https://github.com/caxylive/Net_Projects/blob/main/README.md)

---

# Setting Up Campus VLAN

---

## Network Topology



[Back to Top](top)

---

## Configuring Layer 3 Switch (Core)

### 1. Enable IP Routing

* This is required for inter-VLAN communication

```Bash
Switch(config)# ip routing
```

### 2. Create VLANs and Assign IP Addresses:

* Define VLANs and assign the corresponding gateway IP addresses.

```Bash
Core(config)# vlan 10
Core(config-vlan)# name Admin
Core(config)# exit
Core(config)# interface vlan 10
Core(config-if)# ip address 10.1.10.254 255.255.255.0

Core(config)# vlan 20
Core(config-vlan)# name Faculty
Core(config)# exit
Core(config)# interface vlan 20
Core(config-if)# ip address 10.1.20.254 255.255.255.0

Core(config)# vlan 30
Core(config-vlan)# name IT
Core(config)# exit
Core(config)# interface vlan 30
Core(config-if)# ip address 10.1.30.254 255.255.255.0

Core(config)# vlan 100
Core(config-vlan)# name Server
Core(config)# exit
Core(config)# interface vlan 100
Core(config-if)# ip address 10.1.100.254 255.255.255.0
```

### Verify Configuration

* Use the following commands to ensure VLANs are properly configured:

```Bash
Core# show ip interface brief
Core# show vlan brief
```

[Back to Top](top)

---

