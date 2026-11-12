# HashScope 🛡️
### Zero-Trace, Per-Tab Isolated Threat Hunting & Digital Forensics Web Browser
**Architected by [TOJO P THOMAS](https://medium.com/@tojopthomas)** *(Cyber Forensic Analyst | Investigator | Researcher)*

[![Version](https://img.shields.io/badge/version-1.2.0-blue.svg?style=flat-square)](https://github.com/tojo54/hashscope/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey.svg?style=flat-square)](https://tojo54.github.io/hashscope/)
[![Tests](https://img.shields.io/badge/tests-17%20passed-success.svg?style=flat-square)](test-forensic-engine.js)
[![Architecture](https://img.shields.io/badge/RAM%20Cache-10%20MB%20Strict%20Ceiling-critical.svg?style=flat-square)](#zero-trace-ephemeral-ram-architecture)

---

## 🌐 Official Web Portal & Downloads
- **Live Portal**: [https://hashscope.in/](https://hashscope.in/) | [https://tojo54.github.io/hashscope/](https://tojo54.github.io/hashscope/)
- **HashScope WebTrace v2.4.0 (Free Browsing History Analysis & Browser Artifact Examiner)**: [https://github.com/tojo54/HashScope-WebTrace-Browser-History-Analysis](https://github.com/tojo54/HashScope-WebTrace-Browser-History-Analysis)
- **Creator Publications**: [https://medium.com/@tojopthomas](https://medium.com/@tojopthomas)

---

## 🔬 NEW: HashScope WebTrace v2.4.0 — Free Browsing History Analysis & Digital Forensic Browser Examiner

**Official Repository & Releases:** [**github.com/tojo54/HashScope-WebTrace-Browser-History-Analysis**](https://github.com/tojo54/HashScope-WebTrace-Browser-History-Analysis)

**HashScope WebTrace** is a standalone cross-platform digital forensics workstation designed to extract, carve, correlate, and analyze **14+ browser artifact types** across **Google Chrome, Mozilla Firefox, Microsoft Edge, Apple Safari, Internet Explorer 10/11 (ESENT `WebCacheV01.dat`), Tor Browser, Brave, Opera, and Vivaldi** on **Windows, macOS, and Linux** in both **Portable** and **Installer** modes.

- **14+ Forensic Artifact Categories**: Website Visits, Website Visits Timeline, Searches, Downloads, Cookies, Cached Files, Cached Image Gallery, Cached Web Page Viewer, Bookmarks, Logins (Metadata), Form History, Favicons, Thumbnails, Session Data (`SNSS` / `mozLz4`), Browser Settings, Site Settings, Site Storage, Extracted Email Addresses, and URL Category Threat Filter.
- **Deleted History Recovery**: Carves unallocated SQLite Freelist pages, Write-Ahead Logs (`.sqlite-wal`), Rollback Journals, and Windows Volume Shadow Copies (`VSS`).
- **Built-in Forensic Viewers**: Hex / Binary Inspector, JSON Tree Viewer, Apple Binary/XML `bplist00` PLIST Viewer, Time Zone & DST Engine (WebKit, PRTime, Cocoa CoreData, Windows FILETIME, Unix Epoch), and Court-Admissible PDF / XLSX / CSV / HTML / JSON Report Builder with SHA-256 & MD5 Chain-of-Custody Verification.

| Package | Direct Download (`hashscope.in`) | GitHub Release | SHA-256 Checksum |
| :--- | :--- | :--- | :--- |
| **Windows Installer (`Setup.exe`)** | [`HashScope-WebTrace-Setup.exe`](https://hashscope.in/downloads/HashScope-WebTrace-Setup.exe) | [v2.4.0 Release](https://github.com/tojo54/HashScope-WebTrace-Browser-History-Analysis/releases/tag/v2.4.0) | `CE50C09943E46DC0AA4333A9B6D4BE933BE10FBE54C1E39197809BDB1D0F9EAB` |
| **Windows Portable (`Portable.exe`)** | [`HashScope-WebTrace-Portable.exe`](https://hashscope.in/downloads/HashScope-WebTrace-Portable.exe) | [v2.4.0 Release](https://github.com/tojo54/HashScope-WebTrace-Browser-History-Analysis/releases/tag/v2.4.0) | `D9EF78E4350448E72AB5714177DBCE59501072CFF00DD3557548B10B26073E58` |
| **macOS & Linux Portable (`.run`)** | [`HashScope-WebTrace-v2.4.0-macOS-Linux-Portable.run`](https://hashscope.in/downloads/HashScope-WebTrace-v2.4.0-macOS-Linux-Portable.run) | [v2.4.0 Release](https://github.com/tojo54/HashScope-WebTrace-Browser-History-Analysis/releases/tag/v2.4.0) | `92BE585796E928496C23E21729CF2548BC25DA7F57B5617EAA5F453E37DCBF21` |

---

## 📌 What is HashScope?

**HashScope** is a specialized, open-source forensic web browser engineered from the ground up for **Security Operations Center (SOC) Analysts, Incident Responders, Digital Forensics Investigators, and Malware Researchers**.

Standard commercial web browsers (Google Chrome, Microsoft Edge, Mozilla Firefox) are built to remember everything: they write gigabytes of cached images, persistent SQLite history databases, cookies, and crashpad logs to local storage while continuously leaking hardware telemetry and WebRTC IP addresses.

**HashScope enforces an uncompromising 0-byte disk footprint**: all cache and session partitions exist strictly in volatile memory (RAM) and are permanently purged the moment a tab or session is closed.

```
┌────────────────────────────────────────────────────────────────────────┐
│                        HASHSCOPE FORENSIC ARCHITECTURE                 │
├────────────────────────────────────────────────────────────────────────┤
│  Tab 1: Phishing Kit Recon   ──► [🧅 Tor SOCKS5: 9050]   ──► Darkweb  │
│  Tab 2: Ransomware C2 Portal ──► [🛡️ WireGuard: 1080]    ──► Tunnel   │
│  Tab 3: Exploit Interception ──► [🔍 Burp Suite: 8080]   ──► Local    │
│  Tab 4: OSINT Domain Audit   ──► [⚡ Direct Host ISP]    ──► Clearweb │
├────────────────────────────────────────────────────────────────────────┤
│  RAM Ceiling: 10 MB Max  │  Disk Writes: 0 Bytes  │ WebRTC: UDP Blocked│
└────────────────────────────────────────────────────────────────────────┘
```

---

## ⚡ Key Capabilities

### 1. 🛡️ Concurrent Multi-Route Per-Tab Isolation
In commercial browsers, configuring a proxy alters the entire operating system's routing. HashScope compartments each tab inside an independent in-memory session partition:
- **`⚡ Direct`**: Host network adapter for clearweb OSINT and threat lookups.
- **`🧅 Tor SOCKS5 (Port 9050)`**: Multi-hop onion routing for untraceable darkweb investigation.
- **`🛡️ VPN Bridge (Port 1080)`**: Per-tab WireGuard / OpenVPN user-space tunnel without routing your whole PC.
- **`🔍 Burp Suite / OWASP ZAP (Port 8080)`**: Upstream proxy redirection for HTTP/S parameter inspection and exploit analysis.
- **`⚙️ Custom Proxy`**: SOCKS5, HTTP, or HTTPS configurations.

### 2. 💾 0-Byte Disk Footprint (10 MB RAM Ceiling)
- Chromium disk caching, GPU shader caches, IndexedDB, and crashpad crash dumps are hard-disabled.
- Each tab is bound to `session.fromPartition('tab-ephemeral-*')` kept exclusively in volatile RAM.
- Enforces an automated **10 MB memory ceiling**, automatically pruning stale cache items.
- Tab close instantly wipes all partition cookies, tokens, and storage allocations.

### 3. 📱 Anti-Cloaking Device Emulation
Modern phishing kits, credential harvesters, and malicious redirects inspect client user-agents and screen viewports, serving HTTP 404 or redirecting to legitimate sites if a desktop security scanner is detected.
HashScope provides 1-click device emulation:
- **Apple iPhone iOS (Safari)** — Triggers mobile SMS phishing (smishing) kits.
- **Android Mobile (Samsung Galaxy / Google Pixel)** — Triggers APK payload gates.
- **Googlebot Crawler** — Bypasses anti-crawler cloaking.
- **macOS Safari & Linux Firefox** — Bypasses OS-specific delivery filters.

### 4. ✉️ Email Header & EML Forensic Dissector
- Paste raw email headers or drag-and-drop `.eml` files.
- Automatically analyzes sender spoofing discrepancies (`From` vs `Return-Path` vs `Reply-To`).
- Verifies **SPF, DKIM, and DMARC** authentication verdicts.
- Reconstructs the Mail Transfer Agent (MTA) hop latency timeline.
- Neutralizes and defangs all embedded hyperlinks.

### 5. 📜 Windows Event Log Analyzer & Event ID Encyclopedia
- Correlates critical security logs across JSON, CSV, and XML:
  - **4625**: Failed logon attempts (Brute Force pattern detection).
  - **4688**: Process execution with command-line auditing (Mimikatz, Certutil, encoded PowerShell).
  - **4624**: Successful logons (Type 10 RemoteInteractive / RDP analysis).
  - **1102**: Audit log clearing (Attacker anti-forensics).
  - **4761**: Account member added to security-enabled local group.
- **Integrated Encyclopedia**: Instant lookups with direct reference to **UltimateWindowsSecurity Encyclopedia**.

### 6. ⚖️ ISO/IEC 27037 Court-Admissible Evidence Capture
Generate tamper-evident forensic packages with one click:
- Lossless full-page viewport screenshot (`.png`).
- Client-side rendered DOM structure (`.html`).
- X.509 TLS/SSL certificate chain data (`.json`).
- Individual cryptographic **SHA-256 hashes** for each artifact.
- Immutable, timestamped `CHAIN_OF_CUSTODY_MANIFEST.json`.
- Compiles into a single verifiable `.zip` evidence archive.

### 7. 🚫 WebRTC UDP Leak Killswitch & Privacy Shield
- Enforces Chromium's `disable_non_proxied_udp` policy (RFC 8828), eliminating real local/public IP leaks when routing over VPN or Tor.
- Drops surveillance telemetry scripts (Google Analytics, Facebook Pixel, Hotjar).
- Strips URL query tracking parameters (`fbclid`, `gclid`, `utm_*`).
- Integrated 1-click **Live URL Defanger** (`hxxps[://]`).

### 8. ☢️ Emergency Burn / Nuke
- Single-click emergency killswitch immediately zeroes all active tab RAM, flushes memory buffers, closes all partition webviews, and terminates the application process.

---

## 📦 Verified Release Packages

| Platform | Package | Size | Verification Checksum (SHA-256) |
| :--- | :--- | :--- | :--- |
| **Windows Installer** | [`HashScope-Setup-1.2.0.exe`](https://tojo54.github.io/hashscope/downloads/HashScope-Setup-1.2.0.exe) | ~80.5 MB | `B2387F497D96F37752F2BC2B8F12614950306A9DE6E9BCB425E9A4F163BACC1F` |
| **Windows Portable** | [`HashScope-Portable-1.2.0.exe`](https://tojo54.github.io/hashscope/downloads/HashScope-Portable-1.2.0.exe) | ~80.2 MB | `1E1A190D8A80F78C5E7B15E45E6B223044CEB99E59D8874E743C15B816368B70` |
| **Linux 64-bit** | [`hashscope-1.2.0.tar.gz`](https://tojo54.github.io/hashscope/downloads/hashscope-1.2.0.tar.gz) | ~103 MB | Native 64-bit ELF executable for Kali / Ubuntu / Arch |

### Verify Checksum in Windows PowerShell:
```powershell
Get-FileHash HashScope-Setup-1.2.0.exe -Algorithm SHA256
```

---

## 🚀 Quick Start Guide

### Windows
1. Download **`HashScope-Setup-1.2.0.exe`** (Installer) or **`HashScope-Portable-1.2.0.exe`** (Single file, no install).
2. Double-click to launch.
3. Task Manager shows **`HashScope.exe`** with the official custom shield icon.

### Kali Linux / Ubuntu
```bash
# Extract and launch native package
tar -xzf hashscope-1.2.0.tar.gz
cd hashscope-1.2.0
chmod +x hashscope
./hashscope
```

---

## 👨‍💻 Architect & Research Lead

**TOJO P THOMAS**  
*Cyber Forensic Analyst | Investigator | Researcher*  
- **Medium Publication**: [medium.com/@tojopthomas](https://medium.com/@tojopthomas)  
- **GitHub**: [@tojo54](https://github.com/tojo54)  
- **Project Repository**: [github.com/tojo54/hashscope](https://github.com/tojo54/hashscope)

---

## 📄 License

This project is licensed under the **MIT License** — open-source and free for digital forensics investigators, SOC teams, academic institutions, and cybersecurity students worldwide.
