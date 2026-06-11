⚙️ DHCP Configuration








Cisco CLI Levels — Quick Reference:







| Prompt               | Level          | How to get There         |
| -------------------- | -------------- | -----------------------: |
| Router>              | User mode      | Default when CLI opens   |
| Router#              | Privileged     | type: enable             |
| Router(config)#      | Global config  | type: configure terminal |
| Router(config-if)#   | Interface mode | type: interface Gi0/0    |
| Router(dhcp-config)# | DHCP pool mode | type: ip dhcp pool NAME  |














Complete Router Configuration:




Router> enable

Router# configure terminal

! --- LAN 1 interface (HR Department) ---

Router(config)# interface GigabitEthernet0/0

Router(config-if)# ip address 192.168.10.1 255.255.255.0

Router(config-if)# no shutdown

Router(config-if)# exit


! --- LAN 2 interface (Finance Department) ---

Router(config)# interface GigabitEthernet0/1

Router(config-if)# ip address 192.168.20.1 255.255.255.0

Router(config-if)# no shutdown

Router(config-if)# exit


! --- Exclude router IPs from being assigned to PCs ---

Router(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.9

Router(config)# ip dhcp excluded-address 192.168.20.1 192.168.20.9


! --- DHCP pool for LAN 1 (HR) ---

Router(config)# ip dhcp pool LAN1_POOL

Router(dhcp-config)# network 192.168.10.0 255.255.255.0

Router(dhcp-config)# default-router 192.168.10.1

Router(dhcp-config)# dns-server 8.8.8.8

Router(dhcp-config)# exit


! --- DHCP pool for LAN 2 (Finance) ---

Router(config)# ip dhcp pool LAN2_POOL

Router(dhcp-config)# network 192.168.20.0 255.255.255.0

Router(dhcp-config)# default-router 192.168.20.1

Router(dhcp-config)# dns-server 8.8.8.8

Router(dhcp-config)# exit


! --- Save configuration ---


Router# write memory


























