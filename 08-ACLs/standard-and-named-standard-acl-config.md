# 🌐 Standard & Named Standard ACL Configuration

This document demonstrates both:

* Standard ACL
* Named Standard ACL

using the same enterprise topology with different filtering scenarios.

---

# 🌐 Topology

```text id="h8f9j3"
PC1   PC2   PC4
  \    |    /
      SW1
       |
      R1
       |
      SW2
     /   \
   PC3   PC5
```

---

# 🌐 IP Addressing

## Network 1 — 192.168.10.0/24

| Device  | IP Address    |
| ------- | ------------- |
| R1 G0/0 | 192.168.10.1  |
| PC1     | 192.168.10.10 |
| PC2     | 192.168.10.20 |
| PC4     | 192.168.10.30 |

---

## Network 2 — 192.168.20.0/24

| Device  | IP Address    |
| ------- | ------------- |
| R1 G0/1 | 192.168.20.1  |
| PC3     | 192.168.20.10 |
| PC5     | 192.168.20.20 |

---

# 🌐 Default Gateways

| Device | Gateway      |
| ------ | ------------ |
| PC1    | 192.168.10.1 |
| PC2    | 192.168.10.1 |
| PC4    | 192.168.10.1 |
| PC3    | 192.168.20.1 |
| PC5    | 192.168.20.1 |

---

# 🌐 Base Router Configuration

```cisco id="wqqw0j"
enable
configure terminal

hostname R1

interface g0/0
 ip address 192.168.10.1 255.255.255.0
 no shutdown

interface g0/1
 ip address 192.168.20.1 255.255.255.0
 no shutdown

end
write memory
```

---

# 1️⃣ Standard ACL Configuration

## Objective

Block only PC1 from accessing Network 192.168.20.0/24.

---

# 🌐 Standard ACL Configuration

```cisco id="v4q0hk"
configure terminal

access-list 1 deny host 192.168.10.10
access-list 1 permit any

interface g0/1
 ip access-group 1 out

end
write memory
```

---

# 🌐 Standard ACL Verification

```cisco id="iwrj1f"
show access-lists
show running-config
show ip interface
```

---

# 🌐 Standard ACL Testing

| Source | Destination | Result    |
| ------ | ----------- | --------- |
| PC1    | PC3         | ❌ Blocked |
| PC1    | PC5         | ❌ Blocked |
| PC2    | PC3         | ✅ Allowed |
| PC4    | PC5         | ✅ Allowed |

---

# 🌐 Important Point

Standard ACL filters:

* Source IP address only

Best practice:

```text id="zwx6qn"
Place Standard ACL close to destination
```

---

# 🌐 Remove Standard ACL Before Next Scenario

```cisco id="fksy8h"
configure terminal

interface g0/1
 no ip access-group 1 out

no access-list 1

end
write memory
```

---

# 2️⃣ Named Standard ACL Configuration

## Objective

Block only PC2 from accessing Network 192.168.20.0/24 using a named ACL.

---

# 🌐 Named Standard ACL Configuration

```cisco id="3ghk1j"
configure terminal

ip access-list standard BLOCK-PC2
 deny host 192.168.10.20
 permit any

interface g0/1
 ip access-group BLOCK-PC2 out

end
write memory
```

---

# 🌐 Named Standard ACL Verification

```cisco id="4cxy3m"
show access-lists
show running-config
show ip interface
```

---

# 🌐 Named Standard ACL Testing

| Source | Destination | Result    |
| ------ | ----------- | --------- |
| PC2    | PC3         | ❌ Blocked |
| PC2    | PC5         | ❌ Blocked |
| PC1    | PC3         | ✅ Allowed |
| PC4    | PC5         | ✅ Allowed |

---

# 🌐 Advantages of Named ACL

| Numbered ACL       | Named ACL          |
| ------------------ | ------------------ |
| Uses numbers       | Uses names         |
| Harder to identify | Easier to identify |
| Less readable      | More readable      |

---

# 🌐 Important ACL Concepts

## Implicit Deny

Every ACL automatically ends with:

```text id="euqf8r"
deny any
```

Traffic not explicitly permitted is automatically denied.

---

# 🌐 Verification Commands

```cisco id="0db1vw"
show access-lists
show running-config
show ip interface
```

---

# 🌐 Skills Demonstrated

* Standard ACL
* Named Standard ACL
* Traffic filtering
* Cisco IOS ACL configuration
* Enterprise security policies
* ACL troubleshooting
