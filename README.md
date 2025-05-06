# CNAM & Spam Tag Detection using Android + OCR

This project aims to detect **improper spam labeling and CNAM (Caller Name)** issues that cannot be addressed solely by STIR/SHAKEN compliance.

---

## 📌 Background

According to [Numeracle's Insight](https://www.numeracle.com/insights/stir-shaken-doesnt-stop-improper-spam-labeling), **STIR/SHAKEN** helps validate caller ID authenticity but does **not** stop legitimate calls from being mislabeled as **spam**.

Even fully authenticated calls can be tagged due to **reputation-based analytics** (volume, patterns, reports).

---

## ❌ Problem

- STIR/SHAKEN attestation does **not influence** spam labeling significantly.
- Carriers apply **independent call labeling** rules.
- No SIP-level method to extract “Spam Likely” / “Scam Risk” tags.
- 
## Problem Summary

- CNAM and spam labels like “Spam Likely”, “Scam Risk”, or “Verified Caller” are determined by the receiving carrier.
- These labels are not transmitted in SIP or RTP packets — they are delivered to the end device over proprietary signaling protocols, and only appear on the screen of the phone receiving the call.
- As someone with over 10 years of hands-on experience with Asterisk, I can state with full confidence: this information is never present in SIP INVITE, headers, or any part of the SIP protocol.
- Therefore, it is technically impossible to detect CNAM or spam tagging using Asterisk or any SIP-based system or proxy (e.g., Kamailio, OpenSIPS, FreeSWITCH).
---

## ✅ Solution

We propose a **hardware-based real-world monitoring** approach:

### 🧩 Architecture Overview

```
VoIP System (Asterisk/STIR)
        |
        v
 Android Device + SIM  --->  Screenshot Capture App
        |                          |
        v                          v
   Incoming Calls        --->    Screenshot (.png)
                                     |
                                     v
                           Centralized OCR Server
                                     |
                                     v
                              CNAM / SPAM Logs (JSON)
```

---

## 🛠 Deliverables

1. **Android App**
   - Captures screenshot on incoming call.
   - Sends image to backend server.

2. **Backend (Dockerized)**
   - OCR service (Tesseract / Vision API).
   - Logging, spam tag parsing, JSON export.

3. **Dashboard UI**
   - View devices, logs, CNAM, “Spam Likely” counts.
   - Export CSV or JSON.

4. **Deployment Docs**
   - Android setup
   - Docker instructions
   - Integration guide

---

## 🧪 Sample Screenshots

![Spam Recognition Feature – Index Support](https://tse1.mm.bing.net/th?id=OIP.dA92PAvQ2l2StpOjG8FDWgHaPV&pid=Api)
![STIR/SHAKEN Diagram](https://tse4.mm.bing.net/th?id=OIP.bF6mgQdeirSogB9Qy4dQ3AHaDn&pid=Api)
![Real-World Labeling](https://tse3.mm.bing.net/th?id=OIP.IOjyDjwaefh-f2G1vjBaIAHaE8&pid=Api)

---

## 📄 Reference

- [Numeracle: STIR/SHAKEN Didn’t Stop Improper Spam Labeling](https://www.numeracle.com/insights/stir-shaken-doesnt-stop-improper-spam-labeling)

---

## 👤 Author

Daniel Ha
