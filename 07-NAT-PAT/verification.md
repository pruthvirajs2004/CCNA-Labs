# 🌐 NAT & PAT Verification

This document contains verification commands and testing procedures for:

* Static NAT
* Dynamic NAT
* PAT (NAT Overload)

---

# 🌐 Verify Interface Status

## On R1

```cisco
show ip interface brief
```

### Expected Result

* G0/0 → up/up
* G0/2 → up/up

---

# 🌐 Verify Routing Table

## On R1

```cisco
show ip route
```

### Expected Route

```text
S* 0.0.0.0/0 via 200.1.1.2
```

---

## On ISP Router

```cisco
show ip route
```

### Expected Route

```text
192.168.10.0/24 via 200.1.1.1
```

---

# 🌐 Verify NAT Configuration

## On R1

```cisco
show running-config | include nat
```

### Expected Output

#### Static NAT

```cisco
ip nat inside source static 192.168.10.10 200.1.1.100
```

---

#### Dynamic NAT

```cisco
ip nat pool PUBLIC_POOL 200.1.1.100 200.1.1.110 netmask 255.255.255.0

ip nat inside source list 1 pool PUBLIC_POOL
```

---

#### PAT

```cisco
ip nat inside source list 1 interface g0/2 overload
```

---

# 🌐 Verify NAT Translations

```cisco
show ip nat translations
```

---

# 🌐 Verify NAT Statistics

```cisco
show ip nat statistics
```

### Verify:

* Total active translations
* Hits increasing
* Interfaces marked as inside/outside

---

# 🌐 Connectivity Testing

## From PC1

```text
ping 8.8.8.2
```

---

## From PC2

```text
ping 8.8.8.2
```

---

# 🌐 Successful Verification Indicates

* Routing is working
* NAT translation is functioning
* Internet simulation is reachable
* End-to-end connectivity established

---

# 🌐 PAT Verification

During PAT verification:

```cisco
show ip nat translations
```

### Expected Behavior

* Multiple private IPs translated
* Single public IP used
* Different port numbers assigned

Example:

```text
192.168.10.10:1025 → 200.1.1.1:3001
192.168.10.20:1030 → 200.1.1.1:3002
```

---

# 🌐 Troubleshooting Commands

## Check Interfaces

```cisco
show ip interface brief
```

---

## Check Routes

```cisco
show ip route
```

---

## Check NAT Entries

```cisco
show ip nat translations
```

---

## Check NAT Statistics

```cisco
show ip nat statistics
```

---

## Check Running Configuration

```cisco
show running-config
```

---

# 🌐 Common Issues

| Issue                | Cause                                |
| -------------------- | ------------------------------------ |
| Ping fails           | Missing route                        |
| NAT not working      | Missing inside/outside configuration |
| No translations      | ACL mismatch                         |
| Return traffic fails | Missing ISP route                    |
| PAT not working      | Missing overload keyword             |

---

# 🌐 Final Result

Successful completion verifies:

* Static NAT functionality
* Dynamic NAT functionality
* PAT overload functionality
* Enterprise internet connectivity simulation
