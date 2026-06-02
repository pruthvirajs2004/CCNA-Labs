=================================

SW1 - show vlan brief

=================================

VLAN Name                             Status    Ports

\---- -------------------------------- --------- -------------------------------

1    default                          active    Fa0/3, Fa0/4, Fa0/5, Fa0/6

&#x20;                                               Fa0/7, Fa0/8, Fa0/9, Fa0/10

&#x20;                                               Fa0/11, Fa0/12, Fa0/13, Fa0/14

&#x20;                                               Fa0/15, Fa0/16, Fa0/17, Fa0/18

&#x20;                                               Fa0/19, Fa0/20, Fa0/21, Fa0/22

&#x20;                                               Fa0/23, Gig0/1, Gig0/2

10   HR                               active    Fa0/1

20   FINANCE                          active    Fa0/2

1002 fddi-default                     active    

1003 token-ring-default               active    

1004 fddinet-default                  active    

1005 trnet-default                    active    



=================================

SW1 - show interfaces trunk

=================================

Port        Mode         Encapsulation  Status        Native vlan

Fa0/24      on           802.1q         trunking      1



Port        Vlans allowed on trunk

Fa0/24      10,20



Port        Vlans allowed and active in management domain

Fa0/24      10,20



Port        Vlans in spanning tree forwarding state and not pruned

Fa0/24      10,20



=================================

SW2 - show vlan brief

=================================

VLAN Name                             Status    Ports

\---- -------------------------------- --------- -------------------------------

1    default                          active    Fa0/3, Fa0/4, Fa0/5, Fa0/6

&#x20;                                               Fa0/7, Fa0/8, Fa0/9, Fa0/10

&#x20;                                               Fa0/11, Fa0/12, Fa0/13, Fa0/14

&#x20;                                               Fa0/15, Fa0/16, Fa0/17, Fa0/18

&#x20;                                               Fa0/19, Fa0/20, Fa0/21, Fa0/22

&#x20;                                               Fa0/23, Gig0/1, Gig0/2

10   HR                               active    Fa0/1

20   Finance                          active    Fa0/2

1002 fddi-default                     active    

1003 token-ring-default               active    

1004 fddinet-default                  active    

1005 trnet-default                    active    



=================================

SW2 - show interfaces trunk

=================================

Port        Mode         Encapsulation  Status        Native vlan

Fa0/24      on           802.1q         trunking      1



Port        Vlans allowed on trunk

Fa0/24      10,20



Port        Vlans allowed and active in management domain

Fa0/24      10,20



Port        Vlans in spanning tree forwarding state and not pruned

Fa0/24      10,20





=================================

Connectivity Test Results

=================================



PC-HR-1 (192.168.10.10)

&#x20;   -> PC-HR-2 (192.168.10.20)

&#x20;   SUCCESS



PC-FIN-1 (192.168.20.10)

&#x20;   -> PC-FIN-2 (192.168.20.20)

&#x20;   SUCCESS



PC-HR-1 (192.168.10.10)

&#x20;   -> PC-FIN-1 (192.168.20.10)

&#x20;   FAILED (Expected)



Result:

VLAN isolation verified successfully.

