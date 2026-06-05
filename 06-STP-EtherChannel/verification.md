# Verification Commands and Outputs

This document contains verification commands used for validating STP and EtherChannel configurations.

---

# 🌐 VLAN Verification

```cisco id="jlwm5c"
show vlan brief
```

Verify:

* VLAN 10 exists
* VLAN 20 exists
* Access ports assigned correctly

---

# 🌐 Trunk Verification

```cisco id="jlwm8a"
show interfaces trunk
```

Verify:

* Trunks are operational
* VLANs allowed across trunks

---

# 🌐 STP Verification

```cisco id="jlwm1v"
show spanning-tree
```

Verify:

* Root Bridge
* Forwarding ports
* Blocking ports

---

# 🌐 EtherChannel Verification

```cisco id="jlwm4y"
show etherchannel summary
```

Expected:

```text id="jlwm7d"
Po1(SU)
Po2(SU)
Po3(SU)
```

---

# 🌐 Connectivity Verification

```cisco id="jlwm0l"
ping
```

Verify:

* Same VLAN communication
* Inter-switch VLAN forwarding

---

# 🎯 Expected Results

| Feature             | Expected Status |
| ------------------- | --------------- |
| VLANs               | Active          |
| Trunks              | Operational     |
| STP                 | Loop-Free       |
| EtherChannel        | Bundled         |
| LACP                | Operational     |
| Static EtherChannel | Operational     |

---

# 📚 Verification Commands Summary

```cisco id="jlwm3j"
show vlan brief
show interfaces trunk
show spanning-tree
show etherchannel summary
```
