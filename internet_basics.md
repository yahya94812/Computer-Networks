# 🌐 Internet Architecture

## 1. What is the Internet?

* Internet = **network of networks**
* Each network = **Autonomous System (AS)**
* AS identified by **ASN**
* ASes are connected using **BGP**

---

## 2. End Systems (Edge)

* Laptops, mobiles, servers
* Do **not route**, only send/receive packets
* Examples: Your phone, Google server

---

## 3. Access / Tier-3 ISPs (Last Mile)

* Connect end users
* Provide Wi-Fi, fiber, mobile data
* Usually use **NAT**
* Buy internet from upstream ISPs

**Examples (India):**

* JioFiber
* Airtel Broadband
* BSNL
* ACT Fibernet

---

## 4. Tier-2 ISPs (Regional / National)

* Large regional backbones
* Connect cities & states
* Peer with some networks
* Still buy transit from Tier-1

**Examples:**

* Airtel Backbone
* Reliance Jio Backbone
* Vodafone Idea
* Tata Communications (regional role)

---

## 5. Tier-1 ISPs (Global Backbone)

* Reach **entire internet without paying**
* Peer only with other Tier-1s
* Own submarine cables & global PoPs

**Examples:**

* Tata Communications 🇮🇳
* NTT
* Lumen (Level 3)
* AT&T, Verizon

---

## 6. Content Provider Networks

* Operate as their own AS
* Own **private global backbones**
* Peer directly with ISPs
* Often bypass Tier-1 ISPs

**Examples:**

* Google (AS15169)
* Amazon AWS
* Netflix
* Meta (Facebook)

---

## 7. Internet Exchange Points (IXPs)

* Neutral locations for traffic exchange
* Reduce cost & latency
* Enable direct peering

**Examples:**

* NIXI (India)
* DE-CIX Mumbai / Frankfurt
* AMS-IX, LINX

---

## 8. BGP (Border Gateway Protocol)

* Connects **Autonomous Systems**
* Advertises IP prefixes + AS_PATH
* Routing based on **policy**, not shortest path
* Prevents loops using AS_PATH

---

## 9. Typical Packet Flow

```
Device
 → Home Router (NAT)
 → Tier-3 ISP
 → Tier-2 ISP
 → IXP / Direct Peering
 → Content Network / Server
```

---

## 10. Key Facts to Remember

* Internet is **decentralized**
* Paths can be **asymmetric**
* Routing = control plane
* Forwarding = data plane
* Cost & business decisions shape routing

---

## 11. One-Line Summary

> The Internet is a collection of autonomous systems interconnected by BGP, exchanging traffic via peering and transit, driven by policy rather than distance.
