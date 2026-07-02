
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


















<img width="1920" height="1080" alt="Screenshot (358)" src="https://github.com/user-attachments/assets/72d0c36a-c203-4845-9304-a4ff36483dbf" />


















## 🔧 Fix

  Multiple users unable to resolve hostnames across the network.

  All users on the affected network are unable to access internal resources or external websites using hostnames. 
  
  Network connectivity by IP address remains functional.

  





Escalate to Tier 2

Issue          : Configured internal DNS server unreachable

Impact         : Multiple users across the office

Confirmed      : Configured DNS server is unreachable

Isolation Test : nslookup google.com 8.8.8.8 resolved successfully, isolating the issue to the organization's DNS server

Started        : [Time of first report]
  

 

  ##  ✅ Verification and Validation

     After Tier 2 restores DNS:
     

1. ping <configured DNS server IP>
✔ DNS server reachable

2. nslookup google.com
✔ DNS resolution successful

3. ping google.com
✔ Hostname resolves and network communication succeeds

4. (Production) nslookup intranet.company.local
✔ Internal hostname resolves successfully























































## 📋 Issue Summary 



| **Category**     | **Details**                                                                                                                                                                                                                                                               |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Problem**      | Users across the organization are unable to resolve any hostnames. Both internal resources and external websites fail to load by name.                                                                                                                                    |
| **Root Cause**   | The organization's **configured DNS server is unavailable** or the **DNS service has stopped**, preventing DNS name resolution.                                                                                                                                           |
| **Symptoms**     | All users are affected. Hostname resolution fails, while connectivity using IP addresses (e.g., `ping 8.8.8.8`) remains successful.                                                                                                                                       |
| **Diagnosis**    | Verified that the configured DNS server was unreachable (`ping <configured DNS server IP>` timed out). `nslookup google.com` failed using the configured DNS server, while `nslookup google.com 8.8.8.8` succeeded, isolating the issue to the organization's DNS server. |
| **Resolution**   |  **Permanent Fix:** Escalate to the Tier 2 / Infrastructure Team to restore the organization's internal DNS service.              |
| **Verification** | After the DNS service was restored, the configured DNS server became reachable, `nslookup google.com` successfully resolved the hostname, and users could again access resources by name. ✅                                                                               |


























Real World ticket:

User complaint

Nobody in our office can open any website. Started about 10 minutes ago.

Root cause

DNS server (Configured Server IP) became unreachable. All DNS queries timed out and entire office affected.

Resolution

Confirmed DNS server unreachable via ping. Applied temp public DNS (8.8.8.8). Escalated to Tier 2 with full diagnostic details. DNS restored — reverted to internal DNS. Verified 

across multiple machines.
