

🔴 Project 2 — DNS Troubleshooting Lab

    5 Scenarios
   Real Tier 1 Incidents










| Scenario                 | User Complaint                        | Possible Cause                                  |
| ------------------------ | ------------------------------------- | ----------------------------------------------- |
| Missing A Record         | Reach server by IP but not name       | Missing A record in DNS                         |
| Wrong DNS Server         | Cannot open any website-others fine   | Configured wrong DNS server                     |
| Internal vs External DNS | Google works but intranet does not    | Different DNS settings for internal vs external |
| Hostname Not Resolving   | New server unreachable by name        | Hostname not added to DNS                       |
| DNS Service Down         | Entire office cannot open any website | DNS service is down                             |









How to make DNS Server Unavailable?

Objective: Simulate a DNS failure on a Windows 11 machine and troubleshoot the issue using basic networking tools. The computer was unable to resolve domain names because an 

invalid DNS server address was configured. Users experienced issues accessing websites using domain names such as www.google.com








Environment used:

Operating System: Windows 11

Network Type: Home Network

Browser: Google Chrome / Microsoft Edge

Command-Line Tool: Command Prompt











Steps to Simulate the Issue:






Step 1: Configure an Invalid DNS Server

1. Open Control Panel.

2. Navigate to:

Network and Internet → Network and Sharing Center → Change Adapter Settings

3.Right-click the active network adapter.

4. Select Properties.
   
5.Double-click Internet Protocol Version 4 (TCP/IPv4).

6. Select: Use the following DNS server addresses
       

7. Enter an invalid DNS server address

   Preferred DNS Server: 10.10.10.10

   Alternate DNS Server: 10.10.10.10

8. Click OK and Save & close all windows.









Step 2: Disable IPv6

1. Open Network Adapter Properties

2. Uncheck: Internet Protocol Version 6 (TCP/IPv6)

3. Click OK.
