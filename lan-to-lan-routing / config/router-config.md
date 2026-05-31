
Step 1 - Router Interface Administratively Down


Problem Summary :- 

Router interface GigabitEthernet0/0 administratively down.




Cause


1. The shutdown command was typed on GigabitEthernet0/0
 which disabled the interface manually.

2.Not all pings failed after shutdown
3. Switches handle same-LAN traffic independently.The router is only involved when traffic needs
to cross from one network to another. So cross LAN ping fails.43. Cross-LAN pings timed out,  same-LAN pings unaffected.




Solution:


1.Re-enabled both router interfaces using no shutdown on GigabitEthernet0/0 and Gi0/1
2. This simulates and interface going from administratively down to up.





Verification:

1. Show ip interface brief inside Router CLI
    to confirm both interfaces are now up.

2. Pinging from LAN 1 to LAN 2 to confirm communication
    is fully restored.
