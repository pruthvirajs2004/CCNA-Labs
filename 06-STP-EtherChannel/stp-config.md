# STP Configuration

This document contains the Spanning Tree Protocol (STP) configuration used in the STP & EtherChannel Lab.

---

# 🌐 VLAN Configuration (All Switches)

```cisco id="jlwm2c"
enable
configure terminal

vlan 10
 name HR

vlan 20
 name Finance

end
write memory
```

---

# 🌐 Access Port Configuration

## SW1

```cisco id="jlwm5v"
interface fa0/10
 switchport mode access
 switchport access vlan 10

interface fa0/11
 switchport mode access
 switchport access vlan 20
```

---

## SW2

```cisco id="jlwm8r"
interface fa0/10
 switchport mode access
 switchport access vlan 10

interface fa0/11
 switchport mode access
 switchport access vlan 20
```

---

## SW3

```cisco id="jlwm0p"
interface fa0/10
 switchport mode access
 switchport access vlan 10

interface fa0/11
 switchport mode access
 switchport access vlan 20
```

---

# 🌐 Trunk Configuration

## SW1

```cisco id="jlwm3g"
interface range fa0/1 - 6
 switchport mode trunk
```

---

## SW2

```cisco id="jlwm6f"
interface range fa0/1 - 6
 switchport mode trunk
```

---

## SW3

```cisco id="jlwm9n"
interface range fa0/1 - 6
 switchport mode trunk
```

---

# 🌐 Root Bridge Configuration

## SW3 as Root Bridge

```cisco id="jlwm1x"
spanning-tree vlan 1 priority 32778
```

---

# ✅ Verification Commands

```cisco id="jlwm4j"
show spanning-tree
show vlan brief
show interfaces trunk
```

---

# 🎯 Concepts Demonstrated

* STP
* Root Bridge Election
* VLAN Trunking
* Loop Prevention
* Redundant Switching Paths
