# Verification Commands and Results

This document contains interface verification, routing table validation, and end-to-end connectivity testing for the VLSM-based IP Addressing and Static Routing Lab.

---

# 🌐 R1 Verification

## Interface Status

```cisco
R1#show ip interface brief

Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.10.25   YES manual up                    up
GigabitEthernet0/1     192.168.10.29   YES manual up                    up
GigabitEthernet0/2     192.168.10.1    YES manual up                    up
Vlan1                  unassigned      YES unset  administratively down down
```

All configured interfaces are operational and functioning correctly.

---

## Routing Table

```cisco
R1#show ip route

Gateway of last resort is not set

     192.168.10.0/24 is variably subnetted, 8 subnets, 3 masks

C       192.168.10.0/29 is directly connected, GigabitEthernet0/2
L       192.168.10.1/32 is directly connected, GigabitEthernet0/2

S       192.168.10.8/29 [1/0] via 192.168.10.26
S       192.168.10.16/29 [1/0] via 192.168.10.30

C       192.168.10.24/30 is directly connected, GigabitEthernet0/0
L       192.168.10.25/32 is directly connected, GigabitEthernet0/0

C       192.168.10.28/30 is directly connected, GigabitEthernet0/1
L       192.168.10.29/32 is directly connected, GigabitEthernet0/1
```

### Observations

* Connected routes are properly learned.
* Static routes successfully point to remote networks.
* WAN interfaces are operational.
* VLSM subnet allocation is functioning correctly.

---

# 🌐 R2 Verification

## Interface Status

```cisco
R2#show ip interface brief

Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.10.26   YES manual up                    up
GigabitEthernet0/1     192.168.10.9    YES manual up                    up
GigabitEthernet0/2     unassigned      YES unset  administratively down down
Vlan1                  unassigned      YES unset  administratively down down
```

All configured interfaces are operational.

---

## Routing Table

```cisco
R2#show ip route

Gateway of last resort is not set

     192.168.10.0/24 is variably subnetted, 6 subnets, 3 masks

S       192.168.10.0/29 [1/0] via 192.168.10.25
C       192.168.10.8/29 is directly connected, GigabitEthernet0/1
L       192.168.10.9/32 is directly connected, GigabitEthernet0/1

S       192.168.10.16/29 [1/0] via 192.168.10.25

C       192.168.10.24/30 is directly connected, GigabitEthernet0/0
L       192.168.10.26/32 is directly connected, GigabitEthernet0/0
```

### Observations

* Static routes are properly configured.
* R2 can reach remote LANs through R1.
* Point-to-point WAN communication is operational.

---

# 🌐 R3 Verification

## Interface Status

```cisco
R3#show ip interface brief

Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.10.30   YES manual up                    up
GigabitEthernet0/1     192.168.10.17   YES manual up                    up
GigabitEthernet0/2     unassigned      YES unset  administratively down down
Vlan1                  unassigned      YES unset  administratively down down
```

All configured interfaces are operational.

---

## Routing Table

```cisco
R3#show ip route

Gateway of last resort is not set

     192.168.10.0/24 is variably subnetted, 6 subnets, 3 masks

S       192.168.10.0/29 [1/0] via 192.168.10.29
S       192.168.10.8/29 [1/0] via 192.168.10.29

C       192.168.10.16/29 is directly connected, GigabitEthernet0/1
L       192.168.10.17/32 is directly connected, GigabitEthernet0/1

C       192.168.10.28/30 is directly connected, GigabitEthernet0/0
L       192.168.10.30/32 is directly connected, GigabitEthernet0/0
```

### Observations

* Remote LAN communication is functioning correctly.
* Static routing is successfully forwarding traffic.
* WAN links between routers are operational.

---

# 📡 End-to-End Connectivity Test

## Ping Verification

```bash
PC1 > ping 192.168.10.18
SUCCESS

PC3 > ping 192.168.10.2
SUCCESS

PC5 > ping 192.168.10.10
SUCCESS
```

### Result

All devices across different LANs can communicate successfully through static routing.

---

# ✅ Verification Summary

| Verification Item        | Status     |
| ------------------------ | ---------- |
| Router Interfaces        | Successful |
| VLSM Addressing          | Successful |
| Static Routing           | Successful |
| WAN Connectivity         | Successful |
| End-to-End Communication | Successful |

---

# 🎯 Skills Validated

* IPv4 Addressing
* VLSM Subnetting
* Static Routing
* Router Configuration
* WAN Connectivity
* Cisco IOS Verification Commands
* Network Troubleshooting
