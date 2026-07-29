
## 🔴 Service 2 - Default Gateway Issues


## 📋 Problem Summary






   PC can communicate on local network but cannot reach internet or other network segments.



   .

## 🔍 Issue


Common causes:

1. Wrong gateway IP configured
   
2. Router interface down
   
3. Gateway device offline
 
4. Gateway IP changed after router replacement


## 🔎 Verify

## C:\> ipconfig

Default Gateway: 192.168.0.250  ← Incorrect

## C:\> ping 192.168.0.250

Request timed out ❌







<img width="1920" height="1080" alt="Screenshot (405)" src="https://github.com/user-attachments/assets/e92a6318-5a31-4339-9f26-c0d849289724" />








































## 🔧 Fix


Change the IPv4 configuration from Manual to Automatic (DHCP)  and configure an correct default gateway.

Settings → Network & Internet → Wi-fi → Hardware properties → IP assignment → Manual → Automatic → Toggle IPv4 to ON



























## ✅ Verification




## C:\> ping 192.168.10.1

Reply ✅  ← Gateway is reachable



## C:\> tracert 8.8.8.8

First hop: 192.168.10.1  ✅ traffic going via gateway

## C:\> ping 8.8.8.8          Reply ✅ Internet connectivity is restored
















<img width="1920" height="1080" alt="Screenshot (408)" src="https://github.com/user-attachments/assets/0168d80b-f632-481f-8872-92a84ae85180" />





























































 ## ➡️ 🔗 Related Lab

➡️ **[Cannot Reach Default Gateway](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%203-connectivity/cannot-ping-gateway.md)**











