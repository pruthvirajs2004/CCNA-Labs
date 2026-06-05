# 🌐 ACL Verification & Troubleshooting

This document contains verification and troubleshooting commands for:

* Standard ACL
* Named Standard ACL
* Numbered Extended ACL
* Named Extended ACL

---

# 🌐 Verify Interface Status

## On R1

```cisco
show ip interface brief
```

### Expected Result

```text
GigabitEthernet0/0    up/up
GigabitEthernet0/1    up/up
```

---

# 🌐 Verify ACL Configuration

## Show All ACLs

```cisco
show access-lists
```

---

# 🌐 Verify Standard ACL

```cisco
show access-lists 1
```

### Expected Output

```text
Standard IP access list 1
    deny host 192.168.10.10
    permit any
```

---

# 🌐 Verify Named Standard ACL

```cisco
show access-lists BLOCK-PC2
```

### Expected Output

```text
Standard IP access list BLOCK-PC2
    deny host 192.168.10.20
    permit any
```

---

# 🌐 Verify Numbered Extended ACL

```cisco
show access-lists 100
```

### Expected Output

```text
Extended IP access list 100
    deny ip host 192.168.10.10 host 192.168.20.10
    permit ip any any
```

---

# 🌐 Verify Named Extended ACL

```cisco
show access-lists BLOCK-WEB
```

### Expected Output

```text
Extended IP access list BLOCK-WEB
    deny tcp host 192.168.10.10 host 192.168.20.10 eq www
    permit ip any any
```

---

# 🌐 Verify ACL Applied to Interface

```cisco
show ip interface g0/0
```

OR

```cisco
show ip interface g0/1
```

---

# 🌐 Expected Output

```text
Inbound access list is BLOCK-WEB
```

OR

```text
Outbound access list is 1
```

depending on the ACL applied.

---

# 🌐 Verify Running Configuration

```cisco
show running-config
```

---

# 🌐 Verify Hit Counts

```cisco
show access-lists
```

### Example

```text
Extended IP access list BLOCK-WEB
    deny tcp host 192.168.10.10 host 192.168.20.10 eq www (5 matches)
    permit ip any any (20 matches)
```

---

# 🌐 Connectivity Testing

## Standard ACL Testing

### PC1 → PC3

```text
ping 192.168.20.10
```

Expected:

```text
Blocked
```

---

### PC2 → PC3

```text
ping 192.168.20.10
```

Expected:

```text
Successful
```

---

# 🌐 Named Standard ACL Testing

### PC2 → PC3

```text
ping 192.168.20.10
```

Expected:

```text
Blocked
```

---

### PC1 → PC3

```text
ping 192.168.20.10
```

Expected:

```text
Successful
```

---

# 🌐 Numbered Extended ACL Testing

### PC1 → PC3

```text
ping 192.168.20.10
```

Expected:

```text
Blocked
```

---

### PC1 → PC5

```text
ping 192.168.20.20
```

Expected:

```text
Successful
```

---

# 🌐 Named Extended ACL Testing

## HTTP Test

From PC1 browser:

```text
http://192.168.20.10
```

Expected:

```text
Blocked
```

---

## ICMP Test

```text
ping 192.168.20.10
```

Expected:

```text
Successful
```

because only HTTP traffic is denied.

---

# 🌐 Important Verification Commands

| Command             | Purpose                   |
| ------------------- | ------------------------- |
| show access-lists   | View ACL rules            |
| show ip interface   | Verify ACL applied        |
| show running-config | Verify full configuration |
| ping                | Test ICMP traffic         |
| HTTP browser test   | Test web filtering        |

---

# 🌐 Troubleshooting Commands

## Check Interface Status

```cisco
show ip interface brief
```

---

## Check ACL Attachment

```cisco
show ip interface
```

---

## Check ACL Entries

```cisco
show access-lists
```

---

## Check Running Config

```cisco
show running-config
```

---

# 🌐 Common ACL Issues

| Issue                        | Cause                      |
| ---------------------------- | -------------------------- |
| Traffic blocked unexpectedly | Missing permit statement   |
| ACL not working              | Applied on wrong interface |
| ACL not matching             | Incorrect wildcard mask    |
| All traffic blocked          | Implicit deny any          |
| HTTP not blocked             | Wrong protocol/port        |

---

# 🌐 Important ACL Concepts

## Implicit Deny

Every ACL automatically ends with:

```text
deny any
```

Traffic not explicitly permitted is automatically denied.

---

# 🌐 ACL Placement Rules

| ACL Type     | Best Placement       |
| ------------ | -------------------- |
| Standard ACL | Close to destination |
| Extended ACL | Close to source      |

---

# 🌐 Final Verification Result

Successful verification confirms:

* ACL filtering works correctly
* Interfaces are properly configured
* Traffic policies are enforced
* Enterprise security rules are functioning
