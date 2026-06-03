# Router Configuration

This document contains the complete router configurations used for the VLSM-based IP Addressing and Static Routing Lab.

---

# 🌐 R1 Configuration

```cisco
enable
configure terminal

hostname R1

interface GigabitEthernet0/0
 ip address 192.168.10.25 255.255.255.252
 no shutdown

interface GigabitEthernet0/1
 ip address 192.168.10.29 255.255.255.252
 no shutdown

interface GigabitEthernet0/2
 ip address 192.168.10.1 255.255.255.248
 no shutdown

ip route 192.168.10.8 255.255.255.248 192.168.10.26
ip route 192.168.10.16 255.255.255.248 192.168.10.30

end
write memory
```

---

# 🌐 R2 Configuration

```cisco
enable
configure terminal

hostname R2

interface GigabitEthernet0/0
 ip address 192.168.10.26 255.255.255.252
 no shutdown

interface GigabitEthernet0/1
 ip address 192.168.10.9 255.255.255.248
 no shutdown

ip route 192.168.10.0 255.255.255.248 192.168.10.25
ip route 192.168.10.16 255.255.255.248 192.168.10.25

end
write memory
```

---

# 🌐 R3 Configuration

```cisco
enable
configure terminal

hostname R3

interface GigabitEthernet0/0
 ip address 192.168.10.30 255.255.255.252
 no shutdown

interface GigabitEthernet0/1
 ip address 192.168.10.17 255.255.255.248
 no shutdown

ip route 192.168.10.0 255.255.255.248 192.168.10.29
ip route 192.168.10.8 255.255.255.248 192.168.10.29

end
write memory
```

---

# 📌 Configuration Summary

| Router | Connected Networks | Static Routes Configured |
| ------ | ------------------ | ------------------------ |
| R1     | LAN1, R1-R2, R1-R3 | LAN2, LAN3               |
| R2     | LAN2, R1-R2        | LAN1, LAN3               |
| R3     | LAN3, R1-R3        | LAN1, LAN2               |

---

# 🎯 Concepts Demonstrated

* Router Interface Configuration
* IPv4 Address Assignment
* VLSM Addressing
* Static Routing
* Point-to-Point WAN Configuration
* Cisco IOS CLI Configuration
* Multi-Router Communication
