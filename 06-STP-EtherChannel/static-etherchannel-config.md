# Static EtherChannel Configuration

This document contains the Static EtherChannel configuration between SW2 and SW3.

---

# 🌐 SW2 Configuration

```cisco id="jlwm0s"
enable
configure terminal

interface range fa0/3 - 4
 channel-group 3 mode on

interface port-channel 3
 switchport mode trunk

end
write memory
```

---

# 🌐 SW3 Configuration

```cisco id="jlwm3u"
enable
configure terminal

interface range fa0/3 - 4
 channel-group 3 mode on

interface port-channel 3
 switchport mode trunk

end
write memory
```

---

# 📌 Static EtherChannel

Using:

```cisco id="jlwm6e"
mode on
```

creates a manual EtherChannel without negotiation.

---

# ✅ Verification Commands

```cisco id="jlwm9l"
show etherchannel summary
show interfaces trunk
```

---

# 📡 Expected Result

```text id="jlwm2b"
Po3(SU)
```

---

# 🎯 Concepts Demonstrated

* Static EtherChannel
* Manual Link Aggregation
* Trunking over EtherChannel
* Redundant Layer 2 Links
