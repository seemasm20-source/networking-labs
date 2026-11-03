# 🧹 DNS Cache: ipconfig /flushdns

[ Back to README] → [README.md](./README.md)

---

> **Lab Note:** All steps below were run on a real Windows machine. The screenshot shows the actual output.

## 📋 Problem Summary

A user can still reach an old or wrong version of a website, or a server that moved to a new IP is still reached at the old address. The DNS record was updated, but the PC keeps using the old cached answer.

---

## 💡 What is the DNS Resolver Cache?

Windows stores recent DNS lookups in a local cache so it does not have to ask the DNS server every time. `ipconfig /flushdns` clears all entries from this cache. The next time a hostname is accessed, Windows performs a fresh DNS lookup.

| When to run `flushdns` | Example |
|---|---|
| Website loads an old or wrong version | The site was updated, but the PC shows the old page |
| Server moved to a new IP | The old IP is still cached |
| DNS record updated | The PC ignores the update |
| New server hostname | The name fails on some PCs only |

> **First triage question:** does the problem affect one PC or everyone? One PC with a stale answer points to the local cache.

---

## 🔎 Verify the Problem

| Test | Command | Result | Meaning |
|------|---------|--------|---------|
| 1. Generate a lookup | `ping google.com` | Reply | The name resolves and the result is cached |
| 2. View the cache | `ipconfig /displaydns` | `google.com` entry shown | The record is stored in the local cache |

---

## 🔧 Fix

### Step 1 – Open Command Prompt as Administrator

Press the **Windows key**, type `cmd`, then select **Run as administrator**.

### Step 2 – Flush the DNS cache

```text
C:\> ipconfig /flushdns
Successfully flushed the DNS Resolver Cache.
```

**Screenshot: DNS cache flushed successfully:**

<img width="1920" height="1080" alt="Screenshot (362)" src="https://github.com/user-attachments/assets/546ae45b-79f3-4cf4-9bc2-2832cddaea18" />

---

## ✅ Verification

| Command | Result |
|---------|--------|
| `ipconfig /displaydns` | The `google.com` entry is gone, so the cache was cleared |
| `ping google.com` | Windows performs a fresh lookup and the name resolves again |

---

## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | A PC uses an old or wrong DNS answer |
| **Cause** | An outdated entry in the local DNS Resolver Cache |
| **Symptom** | Old website version, or a moved server still reached at the old IP |
| **Diagnose** | `ipconfig /displaydns` shows the cached record |
| **Fix** | `ipconfig /flushdns` from an administrator Command Prompt |
| **Verified** | The cached entry is gone and a fresh lookup succeeds |

---

## 💡 Next Step

→ [DNS Cheatsheet](./dns-cheatsheet.md)











