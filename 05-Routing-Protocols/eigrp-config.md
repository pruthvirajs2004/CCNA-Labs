# EIGRP Configuration
This document contains the complete EIGRP configuration used in the Routing Protocols Lab. EIGRP dynamically advertises routes using the DUAL algorithm for loop-free and fast convergence.

---

# 🌐 R1 Configuration
```cisco
enable
configure terminal
hostname Router1

! Interface to SW1 LAN
interface FastEthernet0/1
 ip address 192.168.10.1 255.255.255.248
 no shutdown
exit

! Interface to R2
interface GigabitEthernet0/0
 ip address 192.168.10.25 255.255.255.252
 no shutdown
exit

! Interface to R3
interface GigabitEthernet0/1
 ip address 192.168.10.29 255.255.255.252
 no shutdown
exit

! EIGRP Configuration
router eigrp 10
 network 192.168.10.0 0.0.0.7
 network 192.168.10.24 0.0.0.3
 network 192.168.10.28 0.0.0.3
 no auto-summary
exit

end
write memory
```

---

# 🌐 R2 Configuration
```cisco
enable
configure terminal
hostname Router2

! Interface to SW2 LAN
interface FastEthernet0/1
 ip address 192.168.10.9 255.255.255.248
 no shutdown
exit

! Interface to R1
interface GigabitEthernet0/0
 ip address 192.168.10.26 255.255.255.252
 no shutdown
exit

! EIGRP Configuration
router eigrp 10
 network 192.168.10.8 0.0.0.7
 network 192.168.10.24 0.0.0.3
 no auto-summary
exit

end
write memory
```

---

# 🌐 R3 Configuration
```cisco
enable
configure terminal
hostname Router3

! Interface to SW3 LAN
interface FastEthernet0/1
 ip address 192.168.10.17 255.255.255.248
 no shutdown
exit

! Interface to R1
interface GigabitEthernet0/0
 ip address 192.168.10.30 255.255.255.252
 no shutdown
exit

! EIGRP Configuration
router eigrp 10
 network 192.168.10.16 0.0.0.7
 network 192.168.10.28 0.0.0.3
 no auto-summary
exit

end
write memory
```

---

# 📌 EIGRP Configuration Summary

| Router  | AS Number | Networks Advertised                                          |
|---------|-----------|--------------------------------------------------------------|
| Router1 | 1         | 192.168.10.0/29, 192.168.10.24/30, 192.168.10.28/30         |
| Router2 | 1         | 192.168.10.8/29, 192.168.10.24/30                           |
| Router3 | 1         | 192.168.10.16/29, 192.168.10.28/30                          |

---

# ⚙️ EIGRP Wildcard Masks Used

| Subnet Mask     | Wildcard Mask |
|-----------------|---------------|
| 255.255.255.248 | 0.0.0.7       |
| 255.255.255.252 | 0.0.0.3       |

---

# 🖧 IP Addressing Table

| Device  | Interface   | IP Address      | Subnet Mask     | Gateway         |
|---------|-------------|-----------------|-----------------|-----------------|
| Router1 | Fa0/1       | 192.168.10.1    | 255.255.255.248 | -               |
| Router1 | Gig0/0      | 192.168.10.25   | 255.255.255.252 | -               |
| Router1 | Gig0/1      | 192.168.10.29   | 255.255.255.252 | -               |
| Router2 | Fa0/1       | 192.168.10.9    | 255.255.255.248 | -               |
| Router2 | Gig0/0      | 192.168.10.26   | 255.255.255.252 | -               |
| Router3 | Fa0/1       | 192.168.10.17   | 255.255.255.248 | -               |
| Router3 | Gig0/0      | 192.168.10.30   | 255.255.255.252 | -               |
| PC1     | Fa0         | 192.168.10.2    | 255.255.255.248 | 192.168.10.1    |
| PC2     | Fa0         | 192.168.10.3    | 255.255.255.248 | 192.168.10.1    |
| PC3     | Fa0         | 192.168.10.10   | 255.255.255.248 | 192.168.10.9    |
| PC4     | Fa0         | 192.168.10.11   | 255.255.255.248 | 192.168.10.9    |
| PC5     | Fa0         | 192.168.10.18   | 255.255.255.248 | 192.168.10.17   |
| PC6     | Fa0         | 192.168.10.19   | 255.255.255.248 | 192.168.10.17   |

---

# ✅ Verification Commands
```cisco
show ip eigrp neighbors
show ip eigrp topology
show ip protocols
show ip route
show ip route eigrp
show ip interface brief
```

---

# 📡 Expected Results

After EIGRP configuration:
- Routers dynamically learn remote networks via DUAL algorithm
- EIGRP neighbor relationships established between R1↔R2 and R1↔R3
- EIGRP routes appear with `D` in routing tables
- End-to-end communication succeeds between all LANs

Example:
```text
D    192.168.10.8/29  [90/2172416] via 192.168.10.26, GigabitEthernet0/0
D    192.168.10.16/29 [90/2172416] via 192.168.10.30, GigabitEthernet0/0
```

---

# 🎯 Concepts Demonstrated

- EIGRP Configuration with AS Number
- DUAL (Diffusing Update Algorithm)
- Successor and Feasible Successor Routes
- EIGRP Neighbor Relationships
- Wildcard Mask Configuration
- Dynamic Route Learning
- no auto-summary Command
- Multi-Router Communication
- Cisco IOS Routing Configuration

---

# 🧠 Important EIGRP Concepts

## EIGRP AS Number
All routers must use the **same AS number (10)** to form neighbor relationships.

## EIGRP Metric
EIGRP uses composite metric based on:
- Bandwidth
- Delay
- Reliability (optional)
- Load (optional)

## DUAL Algorithm
- Guarantees **loop-free** paths
- Provides **fast convergence**
- Maintains **Feasible Successor** as backup route

## Advantages of EIGRP
- Faster convergence than OSPF and RIP
- Supports VLSM and CIDR
- Uses partial updates (saves bandwidth)
- Cisco proprietary (supported on all Cisco devices)
- Scalable for medium to large enterprise networks

---

# 🔍 EIGRP Neighbor Verification

```text
Router1# show ip eigrp neighbors

IP-EIGRP neighbors for process 10
H  Address          Interface  Hold  Uptime    SRTT  RTO   Q   Seq
0  192.168.10.26    Gig0/0     12    00:01:20  40    1000  0   5
1  192.168.10.30    Gig0/1     11    00:01:18  40    1000  0   4

Router2# show ip eigrp neighbors
H  Address          Interface  Hold  Uptime    SRTT  RTO   Q   Seq
0  192.168.10.25    Gig0/0     13    00:01:22  40    1000  0   6

Router3# show ip eigrp neighbors
H  Address          Interface  Hold  Uptime    SRTT  RTO   Q   Seq
0  192.168.10.29    Gig0/0     14    00:01:19  40    1000  0   5
```

---

# 🔍 EIGRP Routing Table Verification

```text
Router1# show ip route eigrp

D    192.168.10.8/29  [90/2172416] via 192.168.10.26, 00:01:20, GigabitEthernet0/0
D    192.168.10.16/29 [90/2172416] via 192.168.10.30, 00:01:18, GigabitEthernet0/1

Router2# show ip route eigrp

D    192.168.10.0/29  [90/2172416] via 192.168.10.25, 00:01:22, GigabitEthernet0/0
D    192.168.10.16/29 [90/2684416] via 192.168.10.25, 00:01:22, GigabitEthernet0/0
D    192.168.10.28/30 [90/2172416] via 192.168.10.25, 00:01:22, GigabitEthernet0/0

Router3# show ip route eigrp

D    192.168.10.0/29  [90/2172416] via 192.168.10.29, 00:01:19, GigabitEthernet0/0
D    192.168.10.8/29  [90/2684416] via 192.168.10.29, 00:01:19, GigabitEthernet0/0
D    192.168.10.24/30 [90/2172416] via 192.168.10.29, 00:01:19, GigabitEthernet0/0
```

---

# 🧪 Connectivity Tests

```text
PC1> ping 192.168.10.10   ! PC1 → PC3  ✅ SUCCESS
PC1> ping 192.168.10.11   ! PC1 → PC4  ✅ SUCCESS
PC1> ping 192.168.10.18   ! PC1 → PC5  ✅ SUCCESS
PC1> ping 192.168.10.19   ! PC1 → PC6  ✅ SUCCESS
PC3> ping 192.168.10.18   ! PC3 → PC5  ✅ SUCCESS
PC1> tracert 192.168.10.10 ! Path: PC1 → R1 → R2 → PC3
```
