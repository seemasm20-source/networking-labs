⚙️ DHCP Configuration








Cisco CLI Levels — Quick Reference:







| Prompt               | Level          | How to get There         |
| -------------------- | -------------- | -----------------------: |
| Router>              | User mode      |Default when CLI opens   |
| Router#              | Privileged     |type:enable             |
| Router(config)#      | Global config  |type:configure terminal |
| Router(config-if)#   | Interface mode |type:interface Gi0/0    |
| Router(dhcp-config)# | DHCP pool mode |type:ip dhcp pool NAME  |














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




























<img width="1920" height="1080" alt="Screenshot (299)" src="https://github.com/user-attachments/assets/acef8c66-1f85-4795-aaa2-dad059532dcd" />


















































What Each command does?













| Command                            | Description                               |
| ---------------------------------- | ----------------------------------------- |
| Ip Dhcp Excluded-Address           | Stops router assigning these IPs to PCs   |
| Ip Dhcp Pool LAN1_POOL             | Creates a named DHCP pool                 |
| Network 192.168.10.0 255.255.255.0 | Defines which network this pool serves    |
| Default-Router 192.168.10.1        | Pushes gateway IP to PCs automatically    |
| Dns-Server 8.8.8.8                 | Pushes DNS server IP to PCs automatically |





Note:- Network command uses the NETWORK ADDRESS (.0) i.e 192.168.10.0 and 192.168.20.0 not the router interface IP










Trigger DHCP on Each PC:

Toggle in IP Configuration

Click PC → Desktop → IP Configuration

Click Static → then click DHCP again


















✅ Verification Commands



Verification:1





Check DHCP assignments:



Router# show ip dhcp binding

















| IP Address    | MAC Address               | Type            |
| ------------- | ------------------------- | --------------: |
| 192.168.10.10 | 0002.172B.6053            | Automatic ← PC1 |
| 192.168.10.11 | 0060.2FAC.441D            | Automatic ← PC2 |
| 192.168.10.12 |  000A.F3AA.2B90           | Automatic ← PC3 |
| 192.168.20.10 | 00E0.F7DA.743B            | Automatic ← PC4 |
| 192.168.20.11 | 00D0.FF5D.B94B            | Automatic ← PC5 |
| 192.168.20.12 | 0090.2B20.53D5            | Automatic ← PC6 |













<img width="1920" height="403" alt="Screenshot 1" src="https://github.com/user-attachments/assets/b7ec7ae4-7036-4f0d-aed4-ef5a4147bbb6" />











































Verification:2

Check interfacs are active:

Router# show ip interface brief

GigabitEthernet0/0  192.168.10.1   YES up   up  ✅

GigabitEthernet0/1  192.168.20.1   YES up   up  ✅







































<img width="1920" height="1080" alt="Screenshot (301)" src="https://github.com/user-attachments/assets/45cc07e9-d81d-4378-b2bf-6b93f122b801" />






