
## 🔴 Scenario 1 - Missing A Record





## 📋 Problem Summary

User can reach a server by IP address but cannot reach it by name. All other websites work normally. Only this specific hostname fails.





## 🔍 Issue

Users were unable to access the server using the hostname **server01**. DNS could not resolve the hostname because the required **A Record** was missing or unavailable.

As a result, name based access failed even though network connectivity to a reachable IP address on the network was functional.

### Symptoms

```plaintext
ping server01     → Failed (hostname could not be resolved)

ping 192.168.0.1  → Successful (IP connectivity confirmed)
```

















## 🔎 Verify the Issue

## C:\> ping server01

Ping request could not find host server01

Please check the name and try again.

## C:\> nslookup server01

*** No A or AAAA records available for server01

Findings:

The hostname server01 could not be resolved.

DNS did not return an A Record or AAAA Record.

The issue appears to be related to DNS name resolution.






## Lab Limitation:

This home lab does not contain a production DNS environment or an actual server named server01. The scenario demonstrates the troubleshooting methodology used to identify a potential missing DNS A Record.

In a production environment, additional verification would include testing connectivity directly to the server's IP address to confirm that network connectivity is working while DNS name resolution is failing.




















<img width="1920" height="1080" alt="Screenshot (342)" src="https://github.com/user-attachments/assets/37e5aae0-6e69-4994-9fec-ad594d819aa6" />





















































































## 🔧 Fix
    Escalate to Tier 2 to add A Record in DNS Manager.

    Provide:-

  Hostname  : server01
   
  IP Address: 192.168.10.50
  
  DNS Zone  : company.local
  
 Record Type: A Record
























## ✅ Verification and Validation



After the DNS Administrator creates the required A Record for **server01** the following validation steps should be performed.

### Commands Used

```cmd
nslookup server01
```

```cmd
ping server01
```

### Expected Results

* DNS successfully resolves the hostname **server01** to its assigned IP address.
* `nslookup` returns the correct A Record.
* `ping server01` succeeds.
* Users can access the server using its hostname.








Expected Outcome

The hostname can be resolved successfully through DNS, confirming that the missing A Record issue has been resolved.




















































### Issue Summary













| Issue                                  | Symptom                               | Diagnose                               | Fix                                          | Verified                      |
| -------------------------------------- | ------------------------------------- | -------------------------------------- | -------------------------------------------- | :---------------------------: |
| Server reachable by IP but not by name | ping by name fails & ping by IP works | nslookup returns Non-existent domain | Add A Record in DNS / hosts file temporarily | nslookup returns correct IP ✅ |






















































































User complaint
"I cannot connect to our file server by name. The IP address works fine."

Root cause
A Record missing in DNS, hostname has no IP address entry in DNS database.

Resolution
Confirmed with nslookup Non-existent domain error. Added temporary hosts file entry. Escalated to Tier 2 to create permanent A Record. Verified with nslookup after fix.
