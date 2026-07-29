

## 🔴 Service 3 - Port Blocked Scenarios




## 📋 Problem Summary


  User can ping a server but cannot connect to a specific service. Application fails even though server is reachable.



  ping server    ✅  ← IP connectivity fine
  
  Cannot RDP     ❌  ← port 3389 blocked




  ## 📚 Common Ports


| Port | Protocol | Service                |
| ---- | -------- | ---------------------- |
| 80   | HTTP     | Websites (unencrypted) |
| 443  | HTTPS    | Websites (encrypted)   |
| 53   | DNS      | Name resolution        |
| 3389 | RDP      | Windows Remote Desktop |
| 445  | SMB      | Windows file sharing   |
| 9100 | Print    | Network printing       |
| 22   | SSH      | Secure remote access   |
| 25   | SMTP     | Email sending          |




## 🔧 Fix - RDP Example




Server → Windows Firewall → Advanced → Inbound Rules → Enable Remote Desktop

Or on PC:

Settings  → System  → Remote Desktop →  Connect



