# DHCP And DNS Server Configuration Guide

---

## 1. DHCP Server — Desktop IP Configuration

Navigate to: **Desktop > IP Configuration**

| Field            | Value           |
|------------------|-----------------|
| IP Address       | 192.168.30.3    |
| Subnet Mask      | 255.255.255.0   |
| Default Gateway  | 192.168.30.1    |
| DNS Server       | 192.168.30.3    |

---

## 2. Enable DHCP Service

Navigate to: **Services > DHCP**

- Toggle: **ON**

---

## 3. Pool 1 Configuration

Navigate to: **Services > DHCP**

| Field                    | Value           |
|--------------------------|-----------------|
| Pool Name                | LAN10           |
| Default Gateway          | 192.168.10.1    |
| DNS Server               | 192.168.30.3    |
| Start IP Address         | 192.168.10.10   |
| Subnet Mask              | 255.255.255.0   |
| Maximum Number of Users  | 50              |

> Click **ADD**

---

## 4. Pool 2 Configuration

Navigate to: **Services > DHCP**

| Field                    | Value           |
|--------------------------|-----------------|
| Pool Name                | LAN20           |
| Default Gateway          | 192.168.20.1    |
| DNS Server               | 192.168.30.3    |
| Start IP Address         | 192.168.20.10   |
| Subnet Mask              | 255.255.255.0   |
| Maximum Number of Users  | 50              |

> Click **ADD**

---

## 5. DNS Configuration

Navigate to: **Services > DNS**

- Toggle: **ON**

**Add DNS Record:**

| Field   | Value           |
|---------|-----------------|
| Name    | youtube.com     |
| Address | 192.168.30.2    |

> Click **ADD**

---

## 6. Final Step — Configure PCs

On **all PCs**, navigate to: **Desktop > IP Configuration**

- Select: **DHCP**

Each PC should automatically receive:

- **IP Address**
- **Default Gateway**
- **DNS Server**

---

## 7. Verification

Run the following commands from any PC:

```cmd
ipconfig /all
ping 192.168.30.3
ping 192.168.30.2
ping youtube.com
```
