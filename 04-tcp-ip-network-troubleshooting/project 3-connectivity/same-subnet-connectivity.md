
## 🔴 Connectivity 3 - Same Subnet Cannot Communicate






 ## 📋 Problem Summary


 Two PCs on same network cannot reach each other. Ping between them fails even though both have valid IPs and can reach internet individually.


 ## 🔍 Issue
 
    Possible Cause:
    
1. Windows Firewall blocking ICMP (ping) 

2. Wrong subnet mask on one PC
  
3. Switch or cable issue
 


## 🔎 Verify


PC1 → PC2

C:\> ping 192.168.10.11

Request timed out ❌

Both PCs can ping gateway:

PC1 → Gateway

C:\> ping 192.168.10.1

Reply ✅   Reply from 192.168.10.1: bytes=32 time<1ms TTL=64

** Firewall likely blocking peer-to-peer request




## 🔧 Fix



Control Panel → Windows Defender Firewall

→ Advanced Settings → Inbound Rules

→ Enable: File and Printer Sharing (Echo Request)

→ Enable ICMPv4






## ✅ Verification

PC1 → PC2

C:\> ping 192.168.10.11

Reply from 192.168.10.11 ✅




 Resolution: Enabled the File and Printer Sharing (Echo Request - ICMPv4-In) inbound rule in Windows Defender Firewall.
 
 This allowed inbound ICMP Echo Requests,  restoring successful ping communication between the two PCs.







