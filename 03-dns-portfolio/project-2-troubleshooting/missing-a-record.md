# 🔴 Scenario 1 - Missing A Record

[← Back to Project 2 README](./README.md)

---

## 📋 Problem Summary

A user can reach a server by IP address but cannot reach it by name. All other websites work normally. Only the hostname **server01** fails.

---

## 💡 What is an A Record?

An A record is a DNS entry that maps a hostname to an IPv4 address. If the record is missing, DNS cannot resolve the name, even though the server itself is reachable by IP.

> **Lab limitation:** This home lab has no production DNS environment and no real server named server01. The scenario demonstrates the troubleshooting method used to identify a missing A record. The fix and verification steps cannot be completed here, because they need a DNS administrator.

---

## 🔧 Create the Problem

No setup is needed. The hostname **server01** does not exist in DNS, so the lookup fails on its own.

---

## 🔎 Verify the Problem

### Test 1 - Ping by name

```text
C:\> ping server01

Ping request could not find host server01.
Please check the name and try again.
```

### Test 2 - Query DNS

```text
C:\> nslookup server01

*** No A or AAAA records available for server01
```

### Findings

| Test | Result | Meaning |
|------|--------|---------|
| Ping by name | Failed | The hostname could not be resolved |
| `nslookup` | No A or AAAA record returned | DNS has no record for server01 |
| Ping by IP (reported by the user) | Works | The network is fine; only name resolution fails |

> The fault is DNS name resolution, not network connectivity.

**Screenshot: ping and nslookup failing for server01:**

---

## 🔧 Fix

A Tier 1 technician cannot add DNS records, so the ticket is escalated to Tier 2 with these details:

| Field | Value |
|-------|-------|
| **Hostname** | server01 |
| **IP Address** | 192.168.10.50 |
| **DNS Zone** | company.local |
| **Record Type** | A record |

The Tier 2 administrator adds the record in **DNS Manager**.

---

## ✅ Verification

After the A record is created, the same tests are repeated:

```text
C:\> nslookup server01
C:\> ping server01
```

**Expected result:**

| Test | Expected Result |
|------|-----------------|
| `nslookup server01` | Returns 192.168.10.50 |
| `ping server01` | Replies from 192.168.10.50 |
| User access | The server opens by hostname |

---

## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | Server reachable by IP but not by name |
| **Cause** | A record for server01 missing in DNS |
| **Symptom** | Ping by name fails, ping by IP works |
| **Diagnose** | `ping server01` and `nslookup server01` both fail to resolve |
| **Fix** | Escalated to Tier 2 to add the A record in DNS Manager |
| **Verified** | Expected: `nslookup` returns 192.168.10.50 and `ping server01` succeeds |

---

## 💡 Next Step

→ [Scenario 2: Wrong DNS Server](./wrong-dns-server.md)
