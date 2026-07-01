
## 🔴 Scenario 5- DNS Service Down








## 📋 Problem Summary

   Multiple users across the office cannot open any websites or reach servers by name. Issue started suddenly and affects everyone. Ping by IP still works.





## 🔍 Issue

    The DNS server itself is unreachable, DNS service stopped or DNS server machine is offline.




## 🔎 Verify the Issue



C:\> nslookup google.com
DNS request timed out.
*** Can't find server name for 192.168.10.5: Timed out
*** Default servers are not available

C:\> ping 8.8.8.8
Reply from 8.8.8.8  ← internet up — DNS down

C:\> ping 192.168.10.5
Request timed out.  ← DNS server unreachable

C:\> nslookup google.com 8.8.8.8
Address: 142.250.180.46  ✅ public DNS works












Verified configured DNS server using ipconfig /all ✅

  Verified network connectivity (ping 8.8.8.8) ✅
  
  Verified DNS resolution failure (nslookup google.com) ❌





<img width="1920" height="1080" alt="Screenshot (357)" src="https://github.com/user-attachments/assets/ecfa1661-910e-48aa-bddf-a219d7696d94" />

















## 🔧 Fix

  Multiple users unable to resolve hostnames across the network.

  All users on the affected network are unable to access internal resources or external websites using hostnames. 
  
  Network connectivity by IP address remains functional.

  Escalate to Tier 2 with:


  

 
  
  Escalate to Tier 2 with:
Issue    : DNS server unreachable
Impact   : All users — entire office
Confirmed: ping 192.168.10.5 times out
Test     : nslookup google.com 8.8.8.8 works
Started  : [time of first report]
  






  ##  ✅ Verification and Validation

     After Tier 2 restores DNS:
C:\> ping 192.168.10.5
Reply from 192.168.10.5  ✅
C:\> nslookup google.com
Address: 142.250.180.46  ✅
