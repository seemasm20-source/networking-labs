

## Lab Observations:


These are personal observations and discoveries made while building this lab.

Each one taught a real networking concept relevantto IT Help Desk Tier 1 support.















## Observation: 1


 Default Gateway is Only Needed for Cross-LAN Traffic.


 The gateway is only consulted when traffic needs to leave the local network.

 PC1 communicated fine within LAN 1 Default gateway was missing on PC1. Without a gateway, the PC has no exit route to reach other networks.
 It can talk within its own LAN but nothing beyond.

Explanation:
Default gateway = the router's IP address on your LAN




LAN 1 PCs → Default Gateway: 10.0.0.4    (Router Gi0/0)
LAN 2 PCs → Default Gateway: 192.168.1.4 (Router Gi0/1)

Same LAN ping  (10.0.0.1 → 10.0.0.2)  = gateway NOT NEEDED
Cross LAN ping (10.0.0.2 → 192.168.1.1)  = gateway MANDATORY

How to assign Default Gateway?

Click PC → Desktop → IP Configuration → Static
Default Gateway: 10.0.0.4   (for LAN 1 PCs)



Best Practice:

Always configure the gateway on every PC regardless.
The moment any cross network communication is needed
another office, a server, or the  internet it will
fail without a gateway already set.






## Observation: 2 


Shutdown Command Had No Effect on Same-LAN Ping


I typed in shutdown on Gi0/0 and performed the ping test between PC1 and PC2.
Ping worked, and I thought the shutdown command had not applied correctly.

Explanation:
PC1 and PC2 are both connected to LAN 1 (10.0.0.0). Traffic between devices on the same LAN is done directly through the switch without the help of the router. Thus, shutting down the port of the router will have no effect on same LAN traffic.

The right way to perform the test using the shutdown command is as follows:

Shutdown Gi0/0 then ping cross-LAN:
ping 192.168.1.1  ← this MUST go through the router
                  ← this fails when Gi0/0 is down ✅

 

Lesson learned:

| Source IP | Destination IP | Same LAN | Path                               |
| --------- | -------------- | :------: | ---------------------------------- |
| 10.0.0.1  | 10.0.0.2       | Yes      | PC → Switch → PC                   |
| 10.0.0.1  | 192.168.1.1    | No       | PC → Switch → Router → Switch → PC |






Note: Switches handle same-LAN traffic independently. The router is only involved when traffic crosses
       from one network to another.




       



## Observation : 3



One Router Can Have Two Different IP Addresses



I was confused when I had to assign two different
IPs to the same router, one for each interface.
I thought a router should only have one IP address.




Explanation: A router has multiple physical ports called interfaces.
Each interface connects to one network and gets its
own IP address on that network.




Router Gi0/0 → 10.0.0.4    one IP per interface
Router Gi0/1 → 192.168.1.4 one IP per interface

