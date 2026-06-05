# 🌐 Numbered & Named Extended ACL Configuration

This document demonstrates both:

* Numbered Extended ACL
* Named Extended ACL

using the same enterprise topology with different filtering scenarios.

---

# 🌐 Topology

```text id="wx2kg3"
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

```cisco id="gwk8i1"
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

# 1️⃣ Numbered Extended ACL Configuration

## Objective

Block only PC1 from reaching PC3 while allowing all other traffic.

---

# 🌐 Numbered Extended ACL Configuration

```cisco id="r81j0k"
configure terminal

access-list 100 deny ip host 192.168.10.10 host 192.168.20.10
access-list 100 permit ip any any

interface g0/0
 ip access-group 100 in

end
write memory
```

---

# 🌐 Why Applied on G0/0 Inbound?

Extended ACL best practice:

```text id="d4ij89"
Place Extended ACL close to source
```

---

# 🌐 Numbered Extended ACL Testing

| Source | Destination | Result    |
| ------ | ----------- | --------- |
| PC1    | PC3         | ❌ Blocked |
| PC1    | PC5         | ✅ Allowed |
| PC2    | PC3         | ✅ Allowed |
| PC4    | PC5         | ✅ Allowed |

---

# 🌐 Verification Commands

```cisco id="6x7xw0"
show access-lists
show running-config
show ip interface
```

---

# 🌐 Remove Numbered Extended ACL Before Next Scenario

```cisco id="b7qz8y"
configure terminal

interface g0/0
 no ip access-group 100 in

no access-list 100

end
write memory
```

---

# 2️⃣ Named Extended ACL Configuration

## Objective

Block HTTP traffic from PC1 to PC3 while allowing all other traffic.

---

# 🌐 Named Extended ACL Configuration

```cisco id="h4u7tk"
configure terminal

ip access-list extended BLOCK-WEB

 deny tcp host 192.168.10.10 host 192.168.20.10 eq 80
 permit ip any any

interface g0/0
 ip access-group BLOCK-WEB in

end
write memory
```

---

# 🌐 ACL Logic

| Rule               | Meaning           |
| ------------------ | ----------------- |
| deny tcp           | Block TCP traffic |
| host 192.168.10.10 | Source = PC1      |
| host 192.168.20.10 | Destination = PC3 |
| eq 80              | HTTP traffic only |

---

# 🌐 Named Extended ACL Testing

| Traffic Type   | Result    |
| -------------- | --------- |
| PC1 → PC3 HTTP | ❌ Blocked |
| PC1 → PC3 Ping | ✅ Allowed |
| PC2 → PC3 HTTP | ✅ Allowed |

---

# 🌐 Verification Commands

```cisco id="mn34xp"
show access-lists
show running-config
show ip interface
```

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

```text id="hshcvl"
deny any
```

Traffic not explicitly permitted is automatically denied.

---

# 🌐 Important Interview Rule

| ACL Type     | Placement            |
| ------------ | -------------------- |
| Standard ACL | Close to destination |
| Extended ACL | Close to source      |

---

# 🌐 Skills Demonstrated

* Numbered Extended ACL
* Named Extended ACL
* Protocol filtering
* Port-based filtering
* HTTP blocking
* Enterprise traffic control
* Cisco IOS ACL configuration
* ACL troubleshooting
