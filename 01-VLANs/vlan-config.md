\# VLAN Segmentation and 802.1Q Trunking Configuration



\## SW1 Configuration



```cisco

hostname SW1



interface FastEthernet0/1

&#x20;switchport access vlan 10

&#x20;switchport mode access



interface FastEthernet0/2

&#x20;switchport access vlan 20

&#x20;switchport mode access



interface FastEthernet0/24

&#x20;switchport trunk allowed vlan 10,20

&#x20;switchport mode trunk

```



\## SW2 Configuration



```cisco

hostname SW2



interface FastEthernet0/1

&#x20;switchport access vlan 10

&#x20;switchport mode access



interface FastEthernet0/2

&#x20;switchport access vlan 20

&#x20;switchport mode access



interface FastEthernet0/24

&#x20;switchport trunk allowed vlan 10,20

&#x20;switchport mode trunk

```



\## VLAN Mapping



| VLAN ID | VLAN Name | Ports |

| ------- | --------- | ----- |

| 10      | HR        | Fa0/1 |

| 20      | Finance   | Fa0/2 |



\## Trunk Configuration



| Interface | Mode  | Allowed VLANs |

| --------- | ----- | ------------- |

| Fa0/24    | Trunk | 10,20         |



\## Result



\* VLAN 10 hosts successfully communicated across switches.

\* VLAN 20 hosts successfully communicated across switches.

\* Inter-VLAN communication was blocked as expected.

\* 802.1Q trunking successfully extended VLANs across both switches.

\* VLAN segmentation verified successfully.



