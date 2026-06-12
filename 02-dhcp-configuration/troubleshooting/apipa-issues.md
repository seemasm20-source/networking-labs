 Troubleshooting Issue 1 — APIPA (169.254.x.x) Error







 📋 Problem Summary
 
PCs in HR Department (LAN 1) showing APIPA address 169.254.x.x with no internet access. DHCP service on the router was disabled, no IPs assigned automatically.








What is APIPA?

When a PC cannot reach a DHCP server it self-assigns a temporary 169.254.x.x address. This IP cannot communicate with any other device on the network.






🔧 How to Create the Problem:

```
Router> enable

Router# configure terminal

! === Create APIPA Issue ===

Router(config)# no service dhcp

! OR alternatively:

Router(config)# no ip dhcp pool LAN1_POOL

Router(config)# end

Router# write memory
```














<img width="1920" height="1080" alt="Screenshot (304)" src="https://github.com/user-attachments/assets/062ca100-c944-4172-b915-140c56ebd14c" />













































 Impact:

DHCP disabled → No IP address lease received → Windows assigns an APIPA address (`169.254.x.x`) → Network connectivity is limited or unavailable.


















<img width="1920" height="1080" alt="Screenshot (302)" src="https://github.com/user-attachments/assets/efa1df4b-a0bd-45a7-8faa-74aa00e13579" />
























































🔎 Verify the APIPA Issue:


On affected PC → Desktop → Command Prompt:





ipconfig

You will see:

IPv4 Address  : 169.254.45.78  ← APIPA!

Subnet Mask   : 255.255.255.0

Default Gateway: 0.0.0.0


Symptom

169.254.x.x + empty gateway = DHCP failed.




















<img width="1920" height="1080" alt="Screenshot (303)" src="https://github.com/user-attachments/assets/2ae09b4c-d991-470a-9543-6850ff8eeab6" />
















🔧 Fix — Restore DHCP Service:



Router# configure terminal

! === Fix APIPA Issue ===

Router(config)# service dhcp

! Recreate pool for LAN 1

Router(config)# ip dhcp pool LAN1_POOL

Router(dhcp-config)# network 192.168.10.0 255.255.255.0

Router(dhcp-config)# default-router 192.168.10.1

Router(dhcp-config)# dns-server 8.8.8.8

Router(dhcp-config)# exit

Router(config)# end

Router# write memory





<img width="1920" height="1080" alt="Screenshot (305)" src="https://github.com/user-attachments/assets/64185be0-9b54-4d62-b3e6-c8dcf1d162a6" />
















































✅ Renew IP on the PC:

ipconfig /release

ipconfig /renew

ipconfig

Expected after fix:

IPv4 Address   : 192.168.10.10  

Default Gateway: 192.168.10.1

Subnet Mask   : 255.255.255.0
















<img width="1920" height="1080" alt="Screenshot (306)" src="https://github.com/user-attachments/assets/0bd7f3cb-0106-4d6a-bf49-894572c293e6" />





















































<img width="1920" height="1080" alt="Screenshot (307)" src="https://github.com/user-attachments/assets/dbd1df9e-ab8f-4bff-85cb-1fee57756f93" />















































📋 Quick Summary Table:














































| Step             | Command / Action                     | Purpose                                                                                                     |
| ---------------- | ------------------------------------ | ----------------------------------------------------------------------------------------------------------- |
| Create Problem   | no service dhcp                      | Disables the DHCP service on the router, preventing clients from obtaining IP addresses automatically.      |
| Verify Issue     | ipconfig (on PC)                     | Checks the client's IP configuration and confirms whether an APIPA address (169.254.x.x) has been assigned. |
| Fix Problem      | service dhcp + recreate DHCP pool    | Re-enables the DHCP service and restores the DHCP configuration.                                            |
| Renew IP Address |ipconfig /release then ipconfig /renew| Releases the current IP address and requests a new lease                                                  |


















REAL WORLD TICKET:







User complaint

"My PC shows Limited Connectivity. Cannot access internet or shared drives."

Root cause

DHCP service disabled. PC self-assigned 169.254.x.x - unable to communicate.

Resolution

Re-enabled DHCP + recreated pool. Ran ipconfig /renew. IP 192.168.10.10 assigned — connectivity restored.





























