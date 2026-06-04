# OSPF Configuration

This document contains the complete OSPF configuration used in the Routing Protocols Lab. OSPF dynamically advertises routes using link-state routing and SPF calculations for optimal path selection.

---

# 🌐 R1 Configuration

```cisco id="gjlwm8"
enable
configure terminal

hostname R1

router ospf 1
 network 192.168.10.0 0.0.0.7 area 0
 network 192.168.10.24 0.0.0.3 area 0
 network 192.168.10.28 0.0.0.3 area 0

end
write memory
```

---

# 🌐 R2 Configuration

```cisco id="jlwm5q"
enable
configure terminal

hostname R2

router ospf 1
 network 192.168.10.8 0.0.0.7 area 0
 network 192.168.10.24 0.0.0.3 area 0

end
write memory
```

---

# 🌐 R3 Configuration

```cisco id="jlwm2u"
enable
configure terminal

hostname R3

router ospf 1
 network 192.168.10.16 0.0.0.7 area 0
 network 192.168.10.28 0.0.0.3 area 0

end
write memory
```

---

# 📌 OSPF Configuration Summary

| Router | Process ID | Area   |
| ------ | ---------- | ------ |
| R1     | 1          | Area 0 |
| R2     | 1          | Area 0 |
| R3     | 1          | Area 0 |

---

# ⚙️ OSPF Wildcard Masks Used

| Subnet Mask     | Wildcard Mask |
| --------------- | ------------- |
| 255.255.255.248 | 0.0.0.7       |
| 255.255.255.252 | 0.0.0.3       |

---

# ✅ Verification Commands

```cisco id="jlwm0o"
show ip ospf neighbor
show ip protocols
show ip route
show ip interface brief
```

---

# 📡 Expected Result

After OSPF configuration:

* Routers dynamically learn remote networks
* OSPF neighbor relationships are established
* OSPF routes appear with `O` in routing tables
* End-to-end communication succeeds between all LANs

Example:

```text id="jlwm7v"
O    192.168.10.16/29 [110/2] via 192.168.10.30
```

---

# 🎯 Concepts Demonstrated

* OSPF Configuration
* Link-State Routing
* SPF Algorithm
* OSPF Neighbor Relationships
* Wildcard Mask Configuration
* Dynamic Route Learning
* Multi-Router Communication
* Cisco IOS Routing Configuration

---

# 🧠 Important OSPF Concepts

## OSPF Area 0

Area 0 is the backbone area used for inter-area communication in OSPF.

## OSPF Metric

OSPF uses:

* Cost metric
* Based on bandwidth

## Advantages of OSPF

* Faster convergence
* Scalable
* Supports large enterprise networks
* Efficient route calculation
