

## 🔴 Project 2 - DNS Troubleshooting Lab

    ## 5 Scenarios
   ## Real Tier 1 Incidents










| Scenario                 | User Complaint                        | Possible Cause                                  |
| ------------------------ | ------------------------------------- | ----------------------------------------------- |
| Missing A Record         | Reach server by IP but not name       | Missing A record in DNS                         |
| Wrong DNS Server         | Cannot open any website-others fine   | Configured wrong DNS server                     |
| Internal vs External DNS | Google works but intranet does not    | Different DNS settings for internal vs external |
| Hostname Not Resolving   | New server unreachable by name        | Hostname not added to DNS                       |
| DNS Service Down         | Entire office cannot open any website | DNS service is down                             |





















## How to make DNS Server Unavailable?

Objective: Simulate a DNS failure on a Windows 11 machine and troubleshoot the issue using basic networking tools. 

The computer was unable to resolve domain names because an invalid DNS server address was configured. 

Users experienced issues accessing websites using domain names such as www.google.com.








































































## Environment used:

Operating System: Windows 11

Network Type: Home Network

Browser: Google Chrome / Microsoft Edge

Command-Line Tool: Command Prompt











## Steps to Simulate the Issue:






## Step 1: Configure an Invalid DNS Server

1. Press Windows + I → Network and Internet

2. Navigate to your active connection (Wi-fi or Ethernet)

3. Click on Wi-fi

4. Click on Hardware Properties.

5. Click on DNS server assignment → Edit → Choose manual → Enable IPV4

6. Enter Invalid DNS Server Address:

   Preferred DNS Server: 0.0.0.0

   Alternate DNS Server: 0.0.0.0

9. Click Save & close all windows.


       









## Step 2: Disable IPv6

1. Press Win + R →  type ncpa.cpl

2. Right click your Active Network Adapter

3. Properties  → Uncheck Internet Protocol Version 6 ( TCP/IPV6 )

4. Click OK

