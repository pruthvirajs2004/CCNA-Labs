# Static Routing Configuration

This document contains the complete static routing configuration used in the Routing Protocols Lab. The topology demonstrates VLSM-based subnetting and manual route configuration between multiple routers.

---

# 🌐 R1 Configuration

```cisco id="u3yfj1"
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

```cisco id="mjlwm5"
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

```cisco id="jlwm4m"
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

# 📌 Static Route Summary

| Router | Destination Network | Next Hop      |
| ------ | ------------------- | ------------- |
| R1     | 192.168.10.8/29     | 192.168.10.26 |
| R1     | 192.168.10.16/29    | 192.168.10.30 |
| R2     | 192.168.10.0/29     | 192.168.10.25 |
| R2     | 192.168.10.16/29    | 192.168.10.25 |
| R3     | 192.168.10.0/29     | 192.168.10.29 |
| R3     | 192.168.10.8/29     | 192.168.10.29 |

---

# 🎯 Concepts Demonstrated

* Static Routing
* VLSM Subnetting
* Point-to-Point WAN Addressing
* Multi-Router Communication
* IPv4 Address Planning
* Cisco IOS CLI Configuration
* End-to-End Network Connectivity

---

# ✅ Verification Commands

```cisco id="gqjlwm"
show ip route
show ip interface brief
ping
```

These commands were used to verify successful route installation and network connectivity.
