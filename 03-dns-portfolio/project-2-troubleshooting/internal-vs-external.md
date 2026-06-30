
## Scenario 3 - Internal vs External DNS

> **Lab Note:** This is a simulated enterprise DNS scenario.The internal domain names and IP addresses
>
> are fictional and used to demonstrate IT Support troubleshooting methodology.



## 📋 Problem Summary

User can open external websites like google.com perfectly. 

Cannot reach company intranet or internal servers by name.

Multiple users affected on the same floor.




## 🔍 Issue

 PC using public DNS (8.8.8.8) instead of the company's internal DNS server. Public DNS has no records for internal company hostnames.










## 🔎 Verify the Issue


C:\> nslookup google.com

Addresses: <Public IP returned by DNS>   ✅ External DNS working




C:\> nslookup intranet.company.local

*** 8.8.8.8 can't find intranet.company.local: Non-existent domain














































<img width="1920" height="1080" alt="Screenshot (355)" src="https://github.com/user-attachments/assets/80466807-050e-474a-85f4-f9eebcfcec1d" />

































## 🔧 Fix





1. Press Windows + I → Network and Internet

2. Navigate to your active connection (Wi-fi or Ethernet)

3. Click on Wi-fi

4. Click on Hardware Properties

5. Click on DNS server assignment → Edit → Choose manual → Enable IPV4 → Toggle it ON

6. Enter Invalid DNS Server Address:

   Preferred DNS Server: 10.10.10.10

   Alternate DNS Server:192.168.100.100

9. Click Save & close all windows





## ✅ Verification and Validation

Step:1 Open Command Prompt and clear the DNS cache:

ipconfig /flushdns

Step:2 Verify the new DNS configuration:

ipconfig /all

Step:3 Verify internal DNS resolution:

 nslookup intranet.company.local



## Step:4 Verify external DNS resolution 

 nslookup google.com





## Lab Limitation: This resolution represents the procedure followed in a production enterprise environment. 

Validation of the internal DNS server  requires access to an organization's Active Directory

DNS infrastructure, which was not available in this home lab.









## 📋 Issue Summary































| **Category**     | **Details**                                                                                                                                        |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Problem**      | Unable to access the company intranet while external websites work normally.                                                                       |
| **Root Cause**   | The client was configured to use a **public DNS server**, which has no records for internal company hostnames.                                     |
| **Symptoms**     | External websites (e.g., `google.com`) resolve successfully, but internal hostnames (e.g., `intranet.company.local`) fail to resolve.              |
| **Diagnosis**    | `nslookup intranet.company.local` returned **Non-existent domain**, confirming that the public DNS server could not resolve the internal hostname. |
| **Resolution**   | Updated the client's DNS configuration to use the organization's **internal DNS server** (e.g., `192.168.10.5`).                                   |
| **Verification** | `nslookup intranet.company.local` successfully resolved the hostname after the DNS configuration was updated (production environment). ✅           |





















 Real World IT tickets:


User complaint

"Google works fine but I cannot reach our company intranet or file server."

Root cause

PC configured with public DNS. Public DNS has no records for internal company hostnames.

Resolution

Confirmed with nslookup — public DNS returned Non-existent domain for internal names. Changed DNS to internal server 192.168.10.5. Intranet and file server now resolve correctly.


























