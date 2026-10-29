# 💡 Lab Observations - LAN-to-LAN Routing

[← Back to Project README](./README.md)



## 📝 About This File

These are personal observations and discoveries made while building this lab. Each one taught a real networking concept relevant to IT Help Desk Tier 1 support.



## 💡 Observation 1 - Default Gateway Is Only Needed for Cross-LAN Traffic

PC1 could communicate within LAN 1 even though the default gateway was missing. It only failed when I tried to reach LAN 2.

> The default gateway is only used when traffic leaves the local network.
> Full details in [Wrong Gateway Issue](./troubleshooting/wrong-gateway-issue.md)



The default gateway is the router's IP address on your LAN.

```
LAN 1 PCs → Default Gateway: 10.0.0.4     (Router Gi0/0)
LAN 2 PCs → Default Gateway: 192.168.1.4  (Router Gi0/1)

Same LAN ping  (10.0.0.1 → 10.0.0.2)     = gateway NOT NEEDED
Cross LAN ping (10.0.0.2 → 192.168.1.1)  = gateway MANDATORY
```

**How to assign the default gateway:**

```
Click PC → Desktop → IP Configuration → Static
Default Gateway: 10.0.0.4   (for LAN 1 PCs)
```

**Best Practice:**

Always configure the gateway on every PC regardless. The moment any cross-network communication is needed (another office, a server or the internet) it will fail without a gateway already set.

In real networks the gateway is usually handed out automatically by DHCP, so users rarely type it by hand. That is why a missing gateway on a user PC often points to a DHCP problem or a manual static configuration mistake.

---

## 💡 Observation 2 - Shutdown Had No Effect on Same-LAN Ping

I typed `shutdown` on Gi0/0 and performed the ping test between PC1 and PC2. The ping worked and I thought the shutdown command had not applied correctly.

**Explanation:**

PC1 and PC2 are both on LAN 1 (10.0.0.0/24). Traffic between devices on the same LAN goes directly through the switch without the help of the router. Shutting down the router port therefore has no effect on same-LAN traffic.

**The right way to test the shutdown command:**

Shutdown Gi0/0, then ping cross-LAN:

```
ping 192.168.1.1   ← this MUST go through the router
                   ← this fails when Gi0/0 is down ✅
```

**Observation:**

| Source IP | Destination IP | Same LAN | Path                               |
|-----------|----------------|:--------:|------------------------------------|
| 10.0.0.1  | 10.0.0.2       | Yes      | PC → Switch → PC                   |
| 10.0.0.1  | 192.168.1.1    | No       | PC → Switch → Router → Switch → PC |

> **Note:** Switches handle same-LAN traffic independently. The router is only involved when traffic crosses from one network to another.

---

## 💡 Observation 3 - One Router Can Have Two IP Addresses

I was confused when I had to assign two different IPs to the same router, one for each interface. I thought a router should only have one IP address.

**Observation:**

A router has multiple physical ports called interfaces. Each interface connects to one network and gets its own IP address on that network.

```
Router Gi0/0 → 10.0.0.4      one IP per interface
Router Gi0/1 → 192.168.1.4   one IP per interface
```

> **Lesson learned:** Each router interface is the default gateway for the LAN connected to it. That is why LAN 1 PCs use 10.0.0.4 and LAN 2 PCs use 192.168.1.4. Same router, different interface, different gateway.
