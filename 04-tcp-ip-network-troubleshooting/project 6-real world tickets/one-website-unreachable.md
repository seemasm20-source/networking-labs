
## 🔴 Scenario 3 - One Website unreachable


## 📋 Problem Summary

       User cannot reach one specific website. All other websites load perfectly. Colleagues can reach same site without issues.



## 🔎 Diagnose     

md
C:\> ping 8.8.8.8
Reply from 8.8.8.8  ✅  Internet connectivity works

C:\> ping google.com
Reply from google.com ✅  DNS is working

C:\> ping server1.com
Ping request could not find host example.com ❌
```




## 🔧 Resolution

Flush the local DNS cache:

```cmd
ipconfig /flushdns
```

Output:

```cmd
Windows IP Configuration

Successfully flushed the DNS Resolver Cache.
```

---




## ✅ Verification

```cmd
C:\> ping server1.com

Reply from 93.184.216.34: bytes=32 time=20ms TTL=56
```

The hostname now resolves successfully and the website opens normally in the browser.

---




Note : The issue is isolated to one website on one client. A stale or invalid local DNS cache entry was suspected because only

one website failed to resolve on the affected client, while other websites and other users were unaffected. If unresolved,

continue with Hosts file, browser, proxy/VPN, firewall, content filtering, and routing checks.

