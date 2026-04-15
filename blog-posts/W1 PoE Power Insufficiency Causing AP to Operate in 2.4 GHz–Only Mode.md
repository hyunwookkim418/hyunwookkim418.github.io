## PoE Power Insufficiency Causing AP to Operate in 2.4 GHz–Only Mode

**Last updated:** 1/29/26  

---

## Problem Summary
Several wireless access points were observed operating only on the **2.4 GHz band**, with the **5 GHz radio disabled**.

Initial suspicion pointed to RF configuration or controller settings. However, further investigation revealed the root cause:

> **Insufficient PoE power allocation at the access switch port**

The AP’s 5 GHz radio was disabled not by RF or controller settings, but due to **PoE under-allocation**.

---

## Why it matters?
Modern enterprise APs dynamically adjust functionality based on available power:

- **2.4 GHz → lower power requirement**
- **5 GHz → higher power requirement**
- **PoE under-allocation → AP enters degraded mode**

👉 Result: Reduced wireless performance and capacity

---

## Environment
- **Core Switch:** Cisco Catalyst 9500 (16X 10G Backbone)
- **Access Switch:** Cisco Catalyst 9200L (24 PoE+)
- **Access Point:** Aruba AP-535 (Wi-Fi 6 / 802.11ax)
- **Issue Type:** PoE budget / power negotiation
- **Impact:** Partial wireless degradation (5 GHz unavailable)

---

## Lessons Learned
- PoE is not just power delivery — it directly affects device functionality  
- RF issues can originate from **Layer 1 (electrical constraints)**  
- Always verify **PoE budget and negotiation first** before RF/controller troubleshooting  

---

## Troubleshooting Process

### 1. Identify the Affected Device (L3 → L2 Trace)
```bash
C9500_BB# show arp | include 192.168.123.123
C9500_BB# show mac address-table address 6026.efc0.78b8
```