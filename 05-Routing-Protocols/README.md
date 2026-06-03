# 🌐 Routing Protocols Lab

A hands-on Cisco networking lab demonstrating Static Routing, RIP, OSPF, and EIGRP using Cisco Packet Tracer. This lab focuses on route advertisement, dynamic route learning, VLSM subnetting, and multi-router communication across an enterprise-style topology.

---

# 📚 Lab Objectives

* Configure Static Routing between routers
* Implement RIP Version 2 (RIPv2)
* Configure OSPF dynamic routing
* Configure EIGRP dynamic routing
* Design VLSM-based IP addressing
* Verify routing table learning and end-to-end connectivity
* Compare static and dynamic routing protocols

---

# 🖥️ Network Topology

![Network Topology](topology.png)

This topology demonstrates multi-router communication using both static and dynamic routing protocols in a VLSM-based enterprise network design.

---

# 🌐 Network Design

## LAN Networks

| LAN   | Network Address  | Subnet Mask     | Purpose           |
| ----- | ---------------- | --------------- | ----------------- |
| LAN 1 | 192.168.10.0/29  | 255.255.255.248 | PC1 & PC2 Network |
| LAN 2 | 192.168.10.8/29  | 255.255.255.248 | PC3 & PC4 Network |
| LAN 3 | 192.168.10.16/29 | 255.255.255.248 | PC5 & PC6 Network |

---

## WAN Networks

| Link    | Network Address  | Subnet Mask     |
| ------- | ---------------- | --------------- |
| R1 ↔ R2 | 192.168.10.24/30 | 255.255.255.252 |
| R1 ↔ R3 | 192.168.10.28/30 | 255.255.255.252 |

---

# 📑 IP Addressing Table

| Device | Interface | IP Address       |
| ------ | --------- | ---------------- |
| R1     | G0/0      | 192.168.10.25/30 |
| R1     | G0/1      | 192.168.10.29/30 |
| R1     | G0/2      | 192.168.10.1/29  |
| R2     | G0/0      | 192.168.10.26/30 |
| R2     | G0/1      | 192.168.10.9/29  |
| R3     | G0/0      | 192.168.10.30/30 |
| R3     | G0/1      | 192.168.10.17/29 |
| PC1    | NIC       | 192.168.10.2     |
| PC2    | NIC       | 192.168.10.3     |
| PC3    | NIC       | 192.168.10.10    |
| PC4    | NIC       | 192.168.10.11    |
| PC5    | NIC       | 192.168.10.18    |
| PC6    | NIC       | 192.168.10.19    |

---

# 📚 Routing Protocols Implemented

This lab uses the same enterprise-style topology to demonstrate multiple routing technologies.

## Protocols Covered

* Static Routing
* RIP Version 2 (RIPv2)
* OSPF
* EIGRP

Each routing protocol is configured and verified separately to compare route learning behavior, scalability, and administrative operation.

---

# 🛠️ Technologies Used

* Cisco Packet Tracer
* IPv4 Addressing
* VLSM
* Static Routing
* RIP Version 2
* OSPF
* EIGRP
* Cisco IOS CLI

---

# ⚙️ Static Routing

Static routing is manually configured using:

```cisco id="8bjlwm"
ip route
```

This method provides complete administrative control over routing paths.

---

# ⚙️ RIP Version 2

RIP Version 2 is configured using:

```cisco id="u6jlwm"
router rip
 version 2
 no auto-summary
```

RIPv2 dynamically advertises routes using hop count as the routing metric.

---

# ⚙️ OSPF

OSPF is configured using:

```cisco id="84s4q2"
router ospf 1
```

OSPF is a link-state routing protocol that uses SPF calculations for optimal path selection.

---

# ⚙️ EIGRP

EIGRP is configured using:

```cisco id="2jlwm8"
router eigrp 100
```

EIGRP provides fast convergence and efficient route calculation using composite metrics.

---

# ✅ Verification Commands

```cisco id="jlwm6f"
show ip route
show ip interface brief
show running-config
ping
```

These commands verify:

* Interface status
* Route learning
* Neighbor relationships
* End-to-end connectivity

---

# 📂 Repository Structure

```text
05-Routing-Protocols/
├── README.md
├── topology.png
├── Routing-Protocols-Lab.pkt
├── static-routing-config.md
├── rip-config.md
├── ospf-config.md
├── eigrp-config.md
└── verification.md
```

---

# 🎯 Skills Demonstrated

* Static Routing
* Dynamic Routing
* RIP Configuration
* OSPF Configuration
* EIGRP Configuration
* VLSM Subnetting
* WAN Addressing
* Cisco Router Configuration
* Routing Table Verification
* Enterprise Network Design Concepts

---

# 👨‍💻 Author

## Pruthvi Raj S

🎓 Networking Enthusiast | CCNA Learner | Cisco Packet Tracer Labs

Passionate about building hands-on networking labs focused on routing, switching, subnetting, VLANs, and enterprise network design concepts using Cisco technologies.

### 🔗 Connect With Me

* GitHub: https://github.com/pruthvirajs2004

---

# 📄 License

This project is licensed under the MIT License.
