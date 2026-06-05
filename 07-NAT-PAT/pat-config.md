# pat-config.md

# 🌐 PAT (NAT Overload) Configuration

## Objective

Configure Port Address Translation (PAT) to allow multiple private hosts to share a single public IP address using different port numbers.

---

# 🌐 PAT Overview

PAT translates:

* Multiple inside local addresses
* Into one inside global address
* Using unique port numbers.

---

# 🌐 Network Used

| Network Type          | Address         |
| --------------------- | --------------- |
| Inside Network        | 192.168.10.0/24 |
| Outside Network       | 200.1.1.0/24    |
| Public Server Network | 8.8.8.0/24      |

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

access-list 1 permit 192.168.10.0 0.0.0.255

ip nat inside source list 1 interface g0/2 overload

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

# 🌐 PC Configuration

## PC1

```text
IP Address: 192.168.10.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.10.1
```

---

## PC2

```text
IP Address: 192.168.10.20
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.10.1
```

---

# 🌐 Server Configuration

```text
IP Address: 8.8.8.2
Subnet Mask: 255.255.255.0
Default Gateway: 8.8.8.1
```

---

# 🌐 Verification Commands

```cisco
show ip nat translations
show ip nat statistics
show ip route
show running-config
```

---

# 🌐 Testing

From PC1:

```text
ping 8.8.8.2
```

From PC2:

```text
ping 8.8.8.2
```

---

# 🌐 Expected Result

* Both PCs successfully reach the external server
* NAT translations appear on R1
* Both hosts share one public IP address:

  ```text
  200.1.1.1
  ```

---

# 🌐 Important PAT Concept

PAT allows:

* Multiple devices
* To share one public IP
* By differentiating sessions using port numbers.

---

# 🌐 Interview Point

## Why is PAT also called NAT Overload?

Because multiple private IP addresses overload a single public IP using unique TCP/UDP port numbers.

---

# 🌐 Skills Demonstrated

* PAT Configuration
* NAT Overload
* ACL Configuration
* WAN Connectivity
* Cisco IOS CLI
* Enterprise Internet Access Simulation
