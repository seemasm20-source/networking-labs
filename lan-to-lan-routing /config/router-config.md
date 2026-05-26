 Router Configuration

Overview
The Cisco 2911 router is configured with two interfaces —
one facing HR (LAN 1) and one facing Finance (LAN 2).
All commands are entered in the Router CLI tab inside
Cisco Packet Tracer.

How to Open Router CLI
1. Click the Router on your Packet Tracer canvas
2. Click the CLI tab at the top of the window
3. Press Enter if prompted to continue
4. You will see: Router>



| Prompt             | Level          | How to get there         |
| ------------------ | -------------- | ------------------------ |
| Router>            | User Mode      | Default when CLI opens   |
| Router#            | Privileged     | type: enable             |
| Router(config)#    | Global Config  | type: configure terminal |
| Router(config-if)# | Interface Mode | type: interface Gi0/0    |




Note- Every command only works at its correct level. If a command has no effect check your prompt first.











Router> enable
Router# configure terminal

! --- LAN 1 interface (HR Department) ---
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 10.0.0.4 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

! --- LAN 2 interface (Finance Department) ---
Router(config)# interface GigabitEthernet0/1
Router(config-if)# ip address 192.168.1.4 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

! --- Save configuration ---
Router# write memory





Note: Note: The default gateway on every PC is the router's IP address on that PC's side.

LAN 1 PCs use 10.0.0.4 — LAN 2 PCs use 192.168.1.4








What Each Command Does in CLI:




| Command                           | What It Does                                         |
| --------------------------------- | ---------------------------------------------------- |
| Enable                            | Enters privileged mode — full access to all commands |
| Configure Terminal                | Enters configuration mode — allows changes           |
| Interface GigabitEthernet0/0      | Selects the port facing LAN 1 (HR)                   |
| Ip Address 10.0.0.4 255.255.255.0 | Assigns IP and subnet mask to this port              |
| No ShutDown                       | Opens the port — Cisco ports are locked by default   |
| Exit                              | Goes back one level to configure next interface      |
| Write Memory                      | Saves config permanently — survives restart          |


