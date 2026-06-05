# static-nat-config.md

# 🌐 Static NAT Configuration

## Objective

Configure one-to-one NAT translation between a private IP and a public IP.

---

# 🌐 NAT Mapping

| Private IP    | Public IP   |
| ------------- | ----------- |
| 192.168.10.10 | 200.1.1.100 |

---

# 🌐 R1 Configuration

```cisco
enable
configure terminal

hostname R1

interface g0/0
 ip address 192.168.10.1 255.255.255.0
 ip nat inside
 no shutdown

interface g0/2
 ip address 200.1.1.1 255.255.255.0
 ip nat outside
 no shutdown

ip route 0.0.0.0 0.0.0.0 200.1.1.2

ip nat inside source static 192.168.10.10 200.1.1.100

end
write memory
```

---

# 🌐 ISP Router Configuration

```cisco
enable
configure terminal

hostname ISP

interface g0/0
 ip address 200.1.1.2 255.255.255.0
 no shutdown

interface g0/1
 ip address 8.8.8.1 255.255.255.0
 no shutdown

ip route 192.168.10.0 255.255.255.0 200.1.1.1

end
write memory
```

---

# 🌐 Verification

```cisco
show ip nat translations
show ip nat statistics
```
