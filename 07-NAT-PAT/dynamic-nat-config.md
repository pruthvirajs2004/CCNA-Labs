# dynamic-nat-config.md

# 🌐 Dynamic NAT Configuration

## Objective

Configure Dynamic NAT using a pool of public IP addresses.

---

# 🌐 NAT Pool

```text
200.1.1.100 - 200.1.1.120
```

---

# 🌐 Remove Static NAT

```cisco
configure terminal

no ip nat inside source static 192.168.10.10 200.1.1.100

end
```

---

# 🌐 Configure Dynamic NAT

```cisco
enable
configure terminal

ip nat pool PUBLIC_POOL 200.1.1.100 200.1.1.120 netmask 255.255.255.0

access-list 1 permit 192.168.10.0 0.0.0.255

ip nat inside source list 1 pool PUBLIC_POOL

end
write memory
```

---

# 🌐 Verification

```cisco
show ip nat translations
show ip nat statistics
```
