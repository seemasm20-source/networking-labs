
## 🔴 Scenario 2 — Wrong DNS Server



## 📋 Problem Summary
User cannot open any website or reach any server by name. Only one user is affected colleagues on same network work fine.

## 🔍 Issue

PC configured with incorrect DNS server IP — pointing to a fake or unreachable server. Every DNS query times out.

Configured DNS: 0.0.0.0  ← does not exist
Real DNS      : 192.168.0.1  


## 🔎 Verify the Issue


C:\> ipconfig /all
DNS Servers: 192.168.10.99   ← wrong IP

C:\> nslookup google.com
*** Request to 192.168.10.99 timed-out

C:\> ping 8.8.8.8
Reply from 8.8.8.8  ← internet works — DNS is problem

C:\> nslookup google.com 8.8.8.8
Address: 142.250.180.46  ✅ works with correct DNS
