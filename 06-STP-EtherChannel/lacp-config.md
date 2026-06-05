# LACP Configuration

This document contains the LACP EtherChannel configuration between SW1 and SW2.

---

# 🌐 SW1 Configuration

```cisco id="jlwm7w"
enable
configure terminal

interface range fa0/1 - 2
 channel-group 1 mode active

interface port-channel 1
 switchport mode trunk

end
write memory
```

---

# 🌐 SW2 Configuration

```cisco id="jlwm2m"
enable
configure terminal

interface range fa0/1 - 2
 channel-group 1 mode passive

interface port-channel 1
 switchport mode trunk

end
write memory
```

---

# 📌 LACP Modes

| Mode    | Function                         |
| ------- | -------------------------------- |
| active  | Actively negotiates EtherChannel |
| passive | Waits for negotiation            |

---

# ✅ Verification Commands

```cisco id="jlwm5h"
show etherchannel summary
show interfaces trunk
```

---

# 📡 Expected Result

```text id="jlwm8k"
Po1(SU)
```

Meaning:

* S = Layer 2
* U = In Use

---

# 🎯 Concepts Demonstrated

* EtherChannel
* LACP
* Link Aggregation
* Redundancy
* Bandwidth Aggregation
