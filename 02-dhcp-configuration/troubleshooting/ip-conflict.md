
Troubleshooting Issue-2


IP Address Conflict (Static vs DHCP)






📋 Problem Summary

PC2 manually assigned static IP 192.168.10.10 , same IP DHCP had already assigned to PC1. IP conflict caused intermittent failures for both devices.





🔧 Router Configuration



enable

configure terminal

interface gigabitEthernet0/0

ip address 192.168.10.1 255.255.255.0

no shutdown

exit

ip dhcp excluded-address 192.168.10.1 192.168.10.9

ip dhcp pool LAN1_POOL

network 192.168.10.0 255.255.255.0

default-router 192.168.10.1

dns-server 8.8.8.8

exit

end

write memory











🔧 How to Create the Problem

Step 1 PC1 Gets IP via DHCP

PC1 → Desktop → IP Configuration → DHCP
ipconfig /all
IP Address     : 192.168.10.10
Subnet Mask    : 255.255.255.0
Default Gateway: 192.168.10.1



