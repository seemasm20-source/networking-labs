
## 🔴 Scenario 4- Hostname Not Resolving (new server added to the network)









## 📋 Problem Summary


       New server(server01) added to network yesterday. Users can reach it by IP but hostname fails. 

       DNS record was created but issue persists on some PCs.




  ## 🔍 Issue

  
        PC has a stale negative cache entry from before the DNS record was created. 
        
        PC keeps using the cached failure result even though DNS now has the correct answer.

        Note: The DNS A Record for the new server has been created successfully.
        
        However, some client computers still contain a stale negative DNS cache (NXDOMAIN-Non existent domain) from earlier lookups performed 
        
        before the record existed. As a result, these clients continue using the cached "hostname not found" response instead of querying the DNS server again.




    ## 🔎 Verify the Issue


    Step: 1   Inspect local DNS cache

             C:\> ipconfig /displaydns

   Step: 2     Query the DNS server

             C:\> nslookup server01

  Step: 3     Verify on another Pc (no cache)

              C:\> nslookup newserver01

 




  ##  🔧 Fix          


     C:\> ipconfig /flushdns
     
    Successfully flushed the DNS Resolver Cache.  


  ## ✅ Verification and Validation

  Step:1    C:\> nslookup newserver01

  Step:2    C:\> ping newserver01

























## Lab Note**
 This scenario describes the standard troubleshooting process used in enterprise environments. Reproducing a stale negative DNS cache requires an internal DNS infrastructure where  DNS records are created after clients have already cached an earlier NXDOMAIN response. The commands shown above demonstrate the troubleshooting methodology rather than a fully reproducible home-lab scenario.






















  ## 📋 Issue Summary




  | **Category**     | **Details**                                                                                                                                                                                           |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Problem**      | The newly added server hostname cannot be resolved on some client PCs, while it works correctly on others.                                                                                            |
| **Root Cause**   | The affected clients contain a **stale negative DNS cache (NXDOMAIN)** from a time before the DNS A Record was created.                                                                               |
| **Symptoms**     | Hostname resolution fails on a few client PCs but succeeds on other clients, indicating the issue is isolated to specific machines.                                                                   |
| **Diagnosis**    | Inspected the local DNS cache using `ipconfig /displaydns` and identified a cached negative DNS entry. Compared results with a fresh client to confirm the DNS server contained the correct A Record. |
| **Resolution**   | Cleared the local DNS cache on the affected client using `ipconfig /flushdns`, forcing Windows to perform a fresh DNS lookup.                                                                         |
| **Verification** | `nslookup newserver01` successfully resolved the hostname to the correct IP address after the DNS cache was cleared. ✅                                                    







































Real World ticket:


User complaint

"I cannot reach the new server by name. My colleague at the next desk can reach it fine."

Root cause

PC had stale negative cache from before A Record was created. Kept using cached failure result.

Resolution

Confirmed stale cache with ipconfig /displaydns. Ran ipconfig /flushdns. Retested — server resolved correctly. User can now reach new server by name.|
