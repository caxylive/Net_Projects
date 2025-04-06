<a name="top"></a>
[Back to Main](https://github.com/caxylive/Net_Projects/blob/main/README.md)

---

# Setting Up Campus VLAN

---

## Introduction

[Back to Top](#top)

---

## Network Topology

![Physical Topology](screenshot/physical-topology.png)

[Back to Top](#top)

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

[Back to Top](#top)

---

## Configuring the Management IP Addresses for Access Layer Switches (S1, S2, and S3)


| Configuration Steps                | For Switch1                                            | For Switch2                                            | For Switch3                                            |
|------------------------------------|--------------------------------------------------------|--------------------------------------------------------|--------------------------------------------------------|
| 1. Enter Privileged Mode           | `Switch1> enable`                                      | `Switch2> enable`                                      | `Switch3> enable`                                      |
| 2. Enter Global Configuration Mode | `Switch1# configure terminal`                          | `Switch2# configure terminal`                          | `Switch3# configure terminal`                          |
| 3. Assign IP Address to VLAN 1     | `Switch1(config)# interface vlan 1`                    | `Switch2(config)# interface vlan 1`                    | `Switch3(config)# interface vlan 1`                    |
| 4. Configure VLAN 1 IP Address     | `Switch1(config-if)# ip address 10.1.1.1 255.255.255.0`| `Switch2(config-if)# ip address 10.1.1.2 255.255.255.0`| `Switch3(config-if)# ip address 10.1.1.3 255.255.255.0`|
| 5. Activate VLAN 1 Interface       | `Switch1(config-if)# no shutdown`                      | `Switch2(config-if)# no shutdown`                      | `Switch3(config-if)# no shutdown`                      |
| 6. Set Default Gateway             | `Switch1(config)# ip default-gateway 10.1.1.254`       | `Switch2(config)# ip default-gateway 10.1.1.254`       | `Switch3(config)# ip default-gateway 10.1.1.254`       |
| 7. Exit Configuration Mode         | `Switch1(config)# end`                                 | `Switch2(config)# end`                                 | `Switch3(config)# end`                                 |
| 8. Save Configuration              | `Switch1# write memory`                                | `Switch2# write memory`                                | `Switch3# write memory`                                |
| 9. Verify IP and Connectivity      | `Switch1# show ip interface brief`                     | `Switch2# show ip interface brief`                     | `Switch3# show ip interface brief`                     |
| 10. Verify Connectivity            | `Switch1# ping 10.1.1.254`                             | `Switch2# ping 10.1.1.254`                             | `Switch3# ping 10.1.1.254`                             |







