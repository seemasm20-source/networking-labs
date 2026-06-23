
## 🔴 Scenario 1 — Missing A Record





## 📋 Problem Summary

User can reach a server by IP address but cannot reach it by name. All other websites work normally. Only this specific hostname fails.














## 🔍 Issue

An A Record for the server hostname does not exist in DNS. DNS has no answer when asked "what is the IP for server01?"




ping server01       ← fails — no DNS record

ping 192.168.0.1  ← works — IP direct







## 🔎 Verify the Issue

C:\> ping server01

Ping request could not find host server01.

C:\> nslookup server01

*** dns.google can't find server01: Non-existent domain

C:\> ping 192.168.10.50


Reply from 192.168.10.50: bytes=32 time<1ms TTL=128











Key Diagnostic: Ping by IP works ✅ but ping by name fails ❌ — DNS record is missing, not a connectivity issue.




































<img width="1920" height="1080" alt="Screenshot (338)" src="https://github.com/user-attachments/assets/8d03868c-4ce7-4c78-a58f-68f3ec482118" />

























































## 🔧 Fix
    Escalate to Tier 2 to add A Record in DNS Manager.

    Provide:

  Hostname  : server01
   
  IP Address: 192.168.0.1
  
  DNS Zone  : company.local
  
 Record Type: A Record
























## ✅ Verification and Validation

After the DNS Administrator created the A Record for server01, DNS resolution was tested using nslookup and ping.

Commands Used:

nslookup server01

ping server01

Results:

- Hostname successfully resolved to 192.168.0.1
- Ping by hostname succeeded.
- Users were able to access the server normally.

Issue resolved successfully.
