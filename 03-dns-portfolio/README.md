          🌐 DNS Portfolio — IT Help Desk Tier 1
              
           Author: Seema              Windows 10/11
                 
           IT Help Desk Tier 1        June 2026











  ## 📌 What is This Portfolio?
   
Hands-on DNS troubleshooting scenarios built and tested on a Windows machine. Every scenario is a real Tier 1 support incident with user complaint, root cause, fix, verification 

and real-world ticket.















## 📁 Portfolio Structure:











| Project   | Topic                     | Key Skills                                       |
| --------- | ------------------------- | ------------------------------------------------ |
| Project 1 | DNS Fundamentals          | What DNS is, how it works, key terms             |
| Project 2 | DNS Troubleshooting Lab   | 5 real-world DNS fault scenarios, dns cheatsheet |
| Project 3 | DNS Cache Troubleshooting | displaydns, flushdns                             |
| Project 4 | NSLOOKUP Lab              | Forward, reverse lookup                          |
















## 🎯 DNS TROUBLESHOOTING MATRIX 
















| **Scenario**                                            | **Root Cause**                                           | **Project**              |
| ------------------------------------------------------- | -------------------------------------------------------- | ------------------------ |
| Cannot open any Website                                 | DNS Service Down                                         | project 2                |
| New Server Unreachable by Name                          | Hostname Not Resolving                                   | project 2                |
| Intranet Website not Loading                            | Incorrect Internal or External DNS Configuration         | project 2                |
| Ping By IP Works, Name Fails                            | Missing or Incorrect "A" Record                          | project 2              |
| Some Websites Work, Some Don't                          | Incorrect DNS Server Configuration                       | project 2                |
| User Sees an Old Version of a Website                   | Stale DNS Cache                                          | project 3                |
| DNS Changes Are Not Reflected After Server Migration    | Outdated DNS Cache Requiring Flush                       | project 3                |
| Cannot Access `fileserver.company.local` Using Hostname | Missing or Incorrect A Record (Forward Lookup Failure)   | project 4                |
| Unable to Identify the Hostname of an IP Address        | Missing or Incorrect PTR Record (Reverse Lookup Failure) | project 4                |






## 📋 Key Commands Quick Reference








| Command                   | What It Does                         |
| ------------------------- | ------------------------------------ |
| ipconfig /all             | Shows Current DNS Server On PC       |
| nslookup hostname         | Tests DNS Name Resolution            |
| nslookup hostname 8.8.8.8 | Queries Specific DNS Server          |
| ping hostname             | Tests Name Resolution + Connectivity |
| ping 8.8.8.8              | Tests Connectivity Without DNS       |
| ipconfig /displaydns      | Shows Current DNS Cache              |
| ipconfig /flushdns        | Clears All DNS Cache Entries         |










