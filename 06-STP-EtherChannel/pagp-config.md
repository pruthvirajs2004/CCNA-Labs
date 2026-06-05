# PAgP Configuration

This document contains the PAgP EtherChannel configuration used in the STP & EtherChannel Lab.

PAgP (Port Aggregation Protocol) is a Cisco proprietary protocol used to negotiate and establish EtherChannel links dynamically between switches.

---

# 🌐 SW2 Configuration

```cisco id="jlwm2r"
enable
configure terminal

interface range fa0/5 - 6
 channel-group 3 mode desirable

interface port-channel 2
 switchport mode trunk

end
write memory
```

---

# 🌐 SW3 Configuration

```cisco id="jlwm5n"
enable
configure terminal

interface range fa0/5 - 6
 channel-group 2 mode auto

interface port-channel 2
 switchport mode trunk

end
write memory
```

---

# 📌 PAgP Modes

| Mode      | Function                         |
| --------- | -------------------------------- |
| desirable | Actively negotiates EtherChannel |
| auto      | Passively waits for negotiation  |

---

# 📡 EtherChannel Formation Logic

| Side A    | Side B    | Result        |
| --------- | --------- | ------------- |
| desirable | auto      | Forms         |
| desirable | desirable | Forms         |
| auto      | auto      | Does NOT form |

---

# ✅ Verification Commands

```cisco id="jlwm8v"
show etherchannel summary
show interfaces trunk
```

---

# 📡 Expected Result

```text id="jlwm1n"
Po2(SU)
```

Meaning:

* S = Layer 2
* U = In Use

---

# 🎯 Concepts Demonstrated

* PAgP Configuration
* Cisco Proprietary EtherChannel
* Dynamic Link Aggregation
* Trunking over EtherChannel
* Redundant Layer 2 Switching

---

# 🧠 Important PAgP Concepts

## PAgP

* Cisco proprietary protocol
* Used for automatic EtherChannel negotiation
* Similar to LACP but Cisco-specific

## Difference Between LACP and PAgP

| Feature           | LACP           | PAgP              |
| ----------------- | -------------- | ----------------- |
| Standard          | IEEE           | Cisco Proprietary |
| Negotiation Modes | active/passive | desirable/auto    |
| Compatibility     | Multi-vendor   | Cisco only        |

---

# 📚 Verification Summary

```cisco id="jlwm4b"
show etherchannel summary
```

Verify:

* Port-channel operational
* Member interfaces bundled
* EtherChannel in use
