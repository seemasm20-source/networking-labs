
🔴 Service 2 - Default Gateway Issues


📋 Problem Summary

   PC can communicate on local network but cannot reach internet or other network segments.



   .

🔍 Issue


Common causes:
1. Wrong gateway IP configured
2. Router interface down
3. Gateway device offline
4. Gateway IP changed after router replacement


🔎 Verify

C:\> ipconfig
Default Gateway: 192.168.10.99  ← wrong!

C:\> ping 192.168.10.99
Request timed out ❌







<img width="1920" height="1080" alt="Screenshot (405)" src="https://github.com/user-attachments/assets/e92a6318-5a31-4339-9f26-c0d849289724" />






















🔧 Fix


Change the IPv4 configuration from Automatic (DHCP) to Manual and configure an incorrect default gateway.

Settings → Network & Internet → Wi-fi → Hardware properties → IP assignment → Manual → Toggle IPv4 to ON















<img width="1920" height="1080" alt="Screenshot (406)" src="https://github.com/user-attachments/assets/44c169cc-19a3-4254-b45f-c7e4b21f4eff" />


















































