

## 🔴 Connectivity 1 — Cannot Ping Gateway



## 📋 Problem Summary

PC has valid IP but cannot ping its default gateway. No internet access. Cannot reach anything outside local subnet.



## 🔎 Verify — Step by Step



## Step 1: Check the Current Network Configuration

Run:

ipconfig /all

Note the working IPv4 configuration, including:

IPv4 address
Subnet mask
Default gateway
DHCP status

The correct IPv4 default gateway in this lab was 192.168.0.1.


Step 2: Create the Issue

Change the IPv4 configuration from Automatic (IP) to Manual and configure an incorrect default gateway.

Example:

IP Address: 192.168.0.200
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.0.250
DNS Server: 8.8.8.8



Step 3: Verify the Configuration

Run:

ipconfig /all

The output showed that the incorrect IPv4 default gateway 192.168.0.250 was configured.




Step 4: Test the Configured Gateway

Run:

ping -4 192.168.0.250

The ping failed because the configured gateway address was incorrect and unreachable.



Step 5: Identify the Root Cause

Compare the configured gateway with the previously recorded working configuration.

Incorrect Gateway: 192.168.0.250 ❌
Correct Gateway: 192.168.0.1 ✅

The incorrect IPv4 default gateway was identified as the cause of the IPv4 connectivity issue.





🔧 Fix


1. Change the IPv4 configuration back to Automatic (DHCP) so that the correct IP address, subnet mask, and default gateway are assigned automatically.

2.Cable issue   → replace cable or try different port

3. Switch port   → move to different port

✅ Verification

C:\> ipconfig /all
C:\> ping 192.168.10.1   Reply ✅
C:\> ping 8.8.8.8         Reply ✅
C:\> ping google.com      Reply ✅
