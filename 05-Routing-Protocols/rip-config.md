# RIP Version 2 Configuration

This document contains the complete RIP Version 2 (RIPv2) configuration used in the Routing Protocols Lab. RIP dynamically advertises routes between routers using hop count as the routing metric.

---

# 🌐 R1 Configuration

```cisco
enable
configure terminal

hostname R1

router rip
 version 2
 no auto-summary
 network 192.168.10.0

end
write memory
```

---

# 🌐 R2 Configuration

```cisco
enable
configure terminal

hostname R2

router rip
 version 2
 no auto-summary
 network 192.168.10.0

end
write memory
```

---

# 🌐 R3 Configuration

```cisco
enable
configure terminal

hostname R3

router rip
 version 2
 no auto-summary
 network 192.168.10.0

end
write memory
```

---

# 📌 RIP Configuration Summary

| Router | RIP Version | Auto Summary | Advertised Network |
| ------ | ----------- | ------------ | ------------------ |
| R1     | Version 2   | Disabled     | 192.168.10.0       |
| R2     | Version 2   | Disabled     | 192.168.10.0       |
| R3     | Version 2   | Disabled     | 192.168.10.0       |

---

# ⚠️ Why `no auto-summary`?

RIPv2 performs automatic classful summarization by default.

Since this lab uses:

* VLSM
* Multiple subnet masks

`no auto-summary` is required to advertise the correct subnet information.

---

# ✅ Verification Commands

```cisco
show ip protocols
show ip route
show ip interface brief
```

---

# 📡 Expected Result

After RIP configuration:

* Routers dynamically learn remote networks
* RIP routes appear with `R` in routing tables
* End-to-end communication succeeds between all LANs

Example:

```text
R    192.168.10.16/29 [120/1] via 192.168.10.30
```

---

# 🎯 Concepts Demonstrated

* Dynamic Routing
* RIP Version 2
* Distance Vector Routing
* Route Advertisement
* Hop Count Metric
* VLSM Support
* Cisco IOS Routing Configuration
* Routing Table Learning
