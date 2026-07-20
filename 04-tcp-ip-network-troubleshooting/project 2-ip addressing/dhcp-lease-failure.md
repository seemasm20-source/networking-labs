
## 🔴 IP Issue 2 — DHCP Lease Failure



## 📋 Problem Summary


A PC had a working IP address but lost it suddenly mid-session. The network was working fine then

stopped without any physical changes. The PC shows 0.0.0.0 or 169.254.x.x after losing its IP.



## 🔍 Quick Overview


DHCP lease lifecycle:

                IP Assigned → Working → Lease expiring → Renewal request

               → DHCP server responds ✅ → Lease extended → Still working

                → DHCP server unreachable ❌ → Lease lost → 0.0.0.0 or APIPA
