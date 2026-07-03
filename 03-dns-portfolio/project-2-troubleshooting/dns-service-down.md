
## 🔴 Scenario 5- DNS Service Down








## 📋 Problem Summary

   Multiple users across the office cannot open any websites or reach servers by name. Issue started suddenly and affects everyone. Ping by IP still works.





## 🔍 Issue

    The DNS server itself is unreachable, DNS service stopped or DNS server machine is offline.




## 🔎 Verify the Issue


 1. Verify DNS resolution using the configured DNS server

  C:\> nslookup google.com

  DNS request timed out.
 
  *** Can't find server name for <configured DNS server IP>: Timed out

  ✔ Verified: The configured DNS server is not responding to DNS queries.



2. Verify network connectivity

    C:\> ping 8.8.8.8

    Reply from 8.8.8.8

  ✔ Verified: Network/Internet connectivity is working.




3. Verify the configured DNS server is reachable

     C:\> ping <configured DNS server IP>

     Request timed out

     (Lab Note: This step requires access to an organization's internal DNS server and could not be validated in the home lab)


    ✔ Verified: The configured DNS server is unreachable.

4. Isolate the issue using a public DNS server

   C:\> nslookup google.com 8.8.8.8

    Server:  dns.google
   
    Address: 8.8.8.8

   Non-authoritative answer:
   
   Name:    google.com
   
   Addresses: <Public IPv4/IPv6 addresses>

✔ Verified: Public DNS successfully resolved google.com, confirming that Internet connectivity is working and the issue is isolated to the organization's configured DNS server.




















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

4. (Production) nslookup server1.company.local
✔ Internal hostname resolves successfully




















 ##  Lab Limitation:

An enterprise DNS server outage could not be reproduced in the home lab. 

Client-side troubleshooting commands and expected production behavior are documented based on standard enterprise support procedures.


































## 📋 Issue Summary 



| **Category**     | **Details**                                                                                                                                                                                                                                                               |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Problem**      | Users across the organization are unable to resolve any hostnames. Both internal resources and external websites fail to load by name.                                                                                                                                    |
| **Root Cause**   | The organization's **configured DNS server is unavailable** or the **DNS service has stopped** preventing DNS name resolution.                                                                                                                                           |
| **Symptoms**     | All users are affected. Hostname resolution fails, while connectivity using IP addresses (e.g., `ping 8.8.8.8`) remains successful.                                                                                                                                       |
| **Diagnosis**    | Verified that the configured DNS server was unreachable (`ping <configured DNS server IP>` timed out). `nslookup google.com` failed using the configured DNS server, while `nslookup google.com 8.8.8.8` succeeded, isolating the issue to the organization's DNS server. |
| **Resolution**   |  **Permanent Fix:** Escalate to the Tier 2 / Infrastructure Team to restore the organization's internal DNS service.              |
| **Verification** | After the DNS service was restored, the configured DNS server became reachable, `nslookup google.com` successfully resolved the hostname and users could again access resources by name. ✅                                                                               |


























Real World ticket:

User complaint

Nobody in our office can open any website. Started about 10 minutes ago.

Root cause

The configured DNS server became unreachable, causing all DNS queries to time out and preventing users across the office from resolving hostnames.

Resolution

Confirmed the configured DNS server was unreachable. Applied a temporary public DNS server (8.8.8.8) as a workaround (where permitted). Escalated the incident to Tier 2 with complete diagnostic details. After the internal DNS service was restored, reverted clients to the organization's DNS server and verified successful DNS resolution across multiple client machines. 
