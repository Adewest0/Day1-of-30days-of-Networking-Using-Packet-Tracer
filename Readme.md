# Day 01 — Basic Cisco Network Topology & Connectivity

## 30 Days Networking Challenge Day 01

---

## 📌 Overview

For **Day 1** of my 30 Days Networking Challenge, I built and configured a basic network infrastructure using **Cisco Packet Tracer**. This lab demonstrates fundamental networking concepts including:

- **Network topology design** with multiple LANs connected via routers
- **Ethernet cabling** (straight-through and cross-over cables)
- **IPv4 addressing** and subnetting
- **DHCP** configuration for automatic IP assignment
- **Cisco Discovery Protocol (CDP)** for neighbor discovery
- **Router and switch configuration** fundamentals

This lab establishes the foundation for more advanced networking concepts in the remaining challenges.

---

## 🎯 Objectives

- ✅ Build a network using 2 routers, 2 switches, and 4 PCs
- ✅ Understand and apply Ethernet cabling logic (straight-through vs. cross-over)
- ✅ Configure basic Cisco router and switch settings
- ✅ Configure IPv4 addressing with proper subnetting
- ✅ Enable router interfaces using the `no shutdown` command
- ✅ Verify directly connected Cisco devices using CDP
- ✅ Save device configurations to startup configuration
- ✅ Document the complete implementation for reproducibility

---

## 🌐 Network Topology

The topology consists of two separate LANs (Local Area Networks) connected through an inter-router link (WAN):

- **LAN 1**: 192.168.1.0/24 (R1, SW1, PC1, PC2)
- **LAN 2**: 192.168.2.0/24 (R2, SW2, PC3, PC4)
- **WAN Link**: 10.0.0.0/30 (R1 G0/1 ↔ R2 G0/1)

### Topology Diagram
See the detailed visual representation: [View Topology Diagram](Topologies/Topology.md)

---

## 🧩 Network Devices

| Device | Model | Quantity | Purpose |
|:------:|:-----:|:--------:|---------|
| Router | Cisco 2911 | 2 | Route traffic between LANs |
| Switch | Cisco 2960 | 2 | Switch frames within LANs |
| PC | End Device | 4 | User workstations |

---

## 🔌 Cabling & Connections

| Connection | Cable Type | Purpose |
|:----------:|:----------:|---------|
| PC → Switch | Copper Straight-Through | Connect end devices to switches |
| Switch → Router | Copper Straight-Through | Connect switches to routers on same network |
| Router → Router | Copper Cross-Over | Connect routers back-to-back (WAN link) |

**Note**: In modern networking, most switches auto-detect cable type; however, understanding correct cabling is fundamental.

---

## 📋 IP Addressing Scheme

### Router Interfaces

| Device | Interface | IP Address | Subnet Mask | Network |
|:------:|:---------:|:----------:|:-----------:|---------|
| R1 | G0/0 | 192.168.1.1 | 255.255.255.0 | LAN 1 |
| R1 | G0/1 | 10.0.0.1 | 255.255.255.252 | WAN Link |
| R2 | G0/0 | 192.168.2.1 | 255.255.255.0 | LAN 2 |
| R2 | G0/1 | 10.0.0.2 | 255.255.255.252 | WAN Link |

### PC Configuration

| Device | IP Address | Gateway | Network | DHCP |
|:------:|:----------:|:-------:|---------|:----:|
| PC1 | DHCP | 192.168.1.1 | LAN 1 | ✅ |
| PC2 | DHCP | 192.168.1.1 | LAN 1 | ✅ |
| PC3 | DHCP | 192.168.2.1 | LAN 2 | ✅ |
| PC4 | DHCP | 192.168.2.1 | LAN 2 | ✅ |

---

## ⚙️ Configuration Summary

### Router Configuration (R1 Example)

```
Router R1:
  - Interface G0/0: 192.168.1.1/24 (LAN 1)
  - Interface G0/1: 10.0.0.1/30 (WAN Link)
  - Enable both interfaces: no shutdown
  - Save configuration: copy running-config startup-config
```

### Switch Configuration

```
Switches (SW1 & SW2):
  - VLAN 1 configuration (default)
  - Port assignments maintained
  - MAC address table learning enabled
```

### PC Configuration

- DHCP enabled on all PCs
- Gateway set to router G0/0 interfaces
- DNS resolution configured

---

## ✅ Verification & Testing

### 1. **Interface Status Verification**
```
show ip interface brief
```
Confirms all interfaces have correct IP addresses and are operational (up).

### 2. **CDP Neighbor Discovery**
```
show cdp neighbors
show cdp neighbors detail
```
Verifies directly connected Cisco devices and Layer 2 connectivity.

### 3. **Switch MAC Address Table**
```
show mac address-table
```
Confirms switches are learning MAC addresses of connected devices.

### 4. **Connectivity Testing**
```
ping <destination-ip>
```
Tests end-to-end communication between devices in different LANs.

---

## 🏗️ Screenshots

### Before Configuration
![Before Configuration](<Screenshots D1/Day 1 before.png>)

### After Configuration
![After Configuration](<Screenshots D1/Day 1 after.png>)

### Configuration Process
![Configuration Modes](<Screenshots D1/Day1 Configuration SS3.png>)

---

## 📁 Project Structure

```
Day1-of-30days-of-Networking-Using-Packet-Tracer-Labs/
│
├── README.md                          # This file
│
├── Topologies/
│   ├── Day 1 Net-config.pkt          # Cisco Packet Tracer topology file
│   └── Topology.md                   # ASCII diagram of network topology
│
├── Configs/
│   ├── R1-config.txt                 # Router 1 running configuration
│   ├── R2-config.txt                 # Router 2 running configuration
│   ├── SW1-config.txt                # Switch 1 running configuration
│   ├── SW2-config.txt                # Switch 2 running configuration
│   └── Verification.txt              # Verification commands and output
│
└── Screenshots D1/
    ├── Day 1 before.png              # Initial topology state
    ├── Day 1 after.png               # Configured topology state
    ├── Day1 Configuration SS3.png     # Configuration process screenshot
    ├── Day1 cdp R1&R2 details 1.png
    ├── Day1 show interfaces 1.png
    ├── Day1 show interfaces 2.png
    └── Day1 using show running-config.png
```

---

## 📚 Key Concepts Practiced

| Concept | Details |
|---------|---------|
| **Subnetting** | Dividing IP networks into smaller subnets (LAN 1: /24, LAN 2: /24, WAN: /30) |
| **Routing** | Configuring routers to forward traffic between different networks |
| **DHCP** | Dynamic Host Configuration Protocol for automatic IP assignment | (Day 3)
| **CDP** | Cisco Discovery Protocol for discovering neighboring Cisco devices |
| **Ethernet Standards** | Understanding UTP cabling and connector types |
| **IOS Configuration** | Basic Cisco IOS command structure and modes |

---

## 🔧 Configuration Files

All device configurations have been saved and are available in the `Configs/` directory:

- [R1 Configuration](Configs/R1-config.txt)
- [R2 Configuration](Configs/R2-config.txt)
- [SW1 Configuration](Configs/SW1-config.txt)
- [SW2 Configuration](Configs/SW2-config.txt)
- [Verification Commands](Configs/Verification.txt)

---

## 📦 Files & Resources

- **Packet Tracer File**: [Day 1 Net-config.pkt](Topologies/Day%201%20Net-config.pkt)
- **Topology Diagram**: [Topology.md](Topologies/Topology.md)

---

## 🎓 Learning Outcomes

By completing this lab, I have:

1. ✅ Gained hands-on experience with Cisco Packet Tracer
2. ✅ Understood basic network topology design
3. ✅ Practiced IPv4 addressing and subnetting
4. ✅ Configured routers and switches from the CLI
5. ✅ Verified network connectivity using multiple methods
6. ✅ Documented network configuration for reproducibility

---

## 📝 Notes

- This lab uses private IP address space (RFC 1918)
- DHCP pools are configured on the routers
- All devices are configured with default gateways
- CDP is enabled by default on Cisco devices
- Configuration has been saved to startup configuration on all devices

---

## 🔗 Related Days

This is **Day 1** of my 30-day networking challenge. Stay tuned for more advanced topics in the upcoming days!

---

**Date Created**: 2026  
**Cisco Packet Tracer Version**: 9.0.0  
**Status**: ✅ Complete and Verified