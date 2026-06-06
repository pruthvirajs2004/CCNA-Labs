# Router1-config.md

```bash
enable
configure terminal

hostname R1

interface gigabitEthernet0/0
 ip address 192.168.10.1 255.255.255.0
 no shutdown

interface gigabitEthernet0/1
 ip address 192.168.20.1 255.255.255.0
 no shutdown

interface gigabitEthernet0/2
 ip address 192.168.30.1 255.255.255.0
 no shutdown
 exit

ip name-server 192.168.30.3


end
write memory
```
