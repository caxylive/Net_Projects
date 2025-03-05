<a name="top"></a>
# CCNA Notes: Duplex Mismatch and Network Performance

---

# Table of Contents

1. [Overview of Duplex Mismatch](#1-overview-of-duplex-mismatch)  
2. [Identifying Duplex Mismatches](#2-identifying-duplex-mismatches)  
3. [Causes of Duplex Mismatches](#3-causes-of-duplex-mismatches)  
4. [Resolving Duplex Mismatches](#4-resolving-duplex-mismatches)  
5. [Troubleshooting Duplex Mismatches](#5-troubleshooting-duplex-mismatches)  
6. [Key Takeaways](#6-key-takeaways)  
7. [Common Issues and Solutions](#7-common-issues-and-solutions)  
8. [Example Scenario](#8-example-scenario)  
9. [Moral of the Story](#9-moral-of-the-story)  

---

## 1. **Overview of Duplex Mismatch**

- **Definition**: A duplex mismatch occurs when two connected devices have different duplex settings (e.g., one is set to half duplex, and the other is set to full duplex).

- **Impact**: Duplex mismatches can cause network performance issues such as:
    - Late collisions
    - CRC errors
    - Runt frames
    - Poor throughput
    - Packet drops

[Back to Top](#top)

---

## 2. **Identifying Duplex Mismatches**
### Symptoms
- Successful pings but with performance issues (e.g., slow response, high latency).
- Errors in interface statistics (e.g., CRC errors, late collisions, runt frames).
- High traffic exacerbates the issue, leading to more errors and collisions.

### Tools for Monitoring
- **Syslog Servers**: Log and monitor network events.
- **Network Management** Applications: Tools like SolarWinds can help detect and resolve duplex mismatches.
- **Extended Ping Test**: Use large datagram sizes to simulate high traffic and observe errors.

[Back to Top](#top)

---

## 3. **Causes of Duplex Mismatches**
- **Auto-Negotiation Failure**: Devices fail to negotiate speed and duplex settings properly.
- **Manual Configuration Mismatch**: One device is manually configured for full duplex, while the other is set to half duplex.
- **Historical Design**: Older devices may default to 10 Mbps half duplex if auto-negotiation fails, while newer devices may default to full duplex.

[Back to Top](#top)

---

## 4. **Resolving Duplex Mismatches**
### **Option 1: Configure Both Sides for Auto-Negotiation**
- Use the following commands on both the router and switch:
``` Cisco_IOS
Router(config)# interface f0/3
Router(config-if)# speed auto
Router(config-if)# duplex auto
```
``` Cisco_IOS
Switch(config)# interface f0/3
Switch(config-if)# speed auto
Switch(config-if)# duplex auto
```

### **Option 2: Hardcode Both Sides**
- Manually configure both devices to the same speed and duplex settings (e.g., 100 Mbps full duplex):
``` Cisco_IOS
Router(config)# interface f0/3
Router(config-if)# speed 100
Router(config-if)# duplex full
```
``` Cisco_IOS
Switch(config)# interface f0/3
Switch(config-if)# speed 100
Switch(config-if)# duplex full
```

[Back to Top](#top)

---

## 5. **Troubleshooting Duplex Mismatches**
### Step 1: Clear Interface Counters
- Use the clear counters command to reset interface statistics:
``` Cisco_IOS
Router# clear counters fastethernet 0/3
```

### Step 2: Monitor Interface Statistics
- Use the show interfaces command to check for errors:
``` Cisco_IOS
Router# show interfaces fastethernet 0/3
```
- Key metrics to monitor:
    - **Input Errors**: Indicates issues with receiving data.
    - **CRC Errors**: Data corruption during transmission.
    - **Frame Errors**: Incorrect frame lengths or formatting.
    - **Collisions**: Especially late collisions in half-duplex environments.
    - **Runts and Giants**: Frames that are too small or too large.
    - **Output Errors**: Issues with transmitting data.

### Step 3: Verify Configuration
- Check the current configuration of the interface:
``` Cisco_IOS
Router# show run interface f0/3
```

[Back to Top](#top)

---

## 6. **Key Takeaways** 
  - **Consistent Configuration**: Ensure both devices have the same speed and duplex settings.
  - **Proper Cabling**: Use high-quality, compatible cables (e.g., Cat5 or Cat6 for 100BASE-TX).
  - **Monitoring Tools**: Use tools like SolarWinds to detect and resolve duplex mismatches.
  - **Auto-Negotiation**: Prefer auto-negotiation, but if it fails, manually configure both devices.

[Back to Top](#top)

---

## 7. **Common Issues and Solutions**
### Issue: Runt Frames
- **Definition**: Ethernet frames smaller than 64 bytes.
- **Cause**: Collisions in half-duplex environments or malfunctioning network interface cards.
- **Solution**: Ensure proper duplex settings and use high-quality cables.

### Issue: Late Collisions
- **Definition**: Collisions that occur after the first 64 bytes of a frame have been transmitted.
- **Cause**: Duplex mismatch or excessive cable length.
- **Solution**: Resolve duplex mismatches and check cable lengths.

[Back to Top](#top)

---

## 8. Example Scenario
### Problem:
- Router 1 is connected to Switch 2950-1.
- Router 1 is set to 100 Mbps half duplex (due to auto-negotiation failure).
- Switch 2950-1 is set to 10 Mbps full duplex.
- This mismatch causes late collisions and CRC errors under high traffic.

### Solution:
- Manually configure both devices to 100 Mbps full duplex:
``` Cisco_IOS
Router(config)# interface f0/3
Router(config-if)# speed 100
Router(config-if)# duplex full
```
``` Cisco_IOS
Switch(config)# interface f0/3
Switch(config-if)# speed 100
Switch(config-if)# duplex full
```

[Back to Top](#top)

---

## 9. Moral of the Story
- **Option 1**: Configure both sides for auto-negotiation.
- **Option 2**: Hardcode both sides to the same speed and duplex settings (e.g., 100 Mbps full duplex).

[Back to Top](#top)
