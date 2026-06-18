# Attack Type → MITRE ATT&CK → Mitigation — RESEARCH SCAFFOLD

> ⚠️ **How to use this (NTU integrity).** This is AI-assisted *research* (Amber):
> a starting map you must (1) **verify** every technique/mitigation ID at
> https://attack.mitre.org, (2) **critically evaluate**, and (3) **rewrite in your
> own words** for the report. Reference this assistance in your implementation/method
> chapter and the GenAI acknowledgement form. Do NOT paste these sentences into the report.
>
> Scope note: cover only the attack types that actually appeared in YOUR EDA
> (`detailed_label` chart from notebook 01). The 10 IoT-23 malicious labels are below.

The 10 IoT-23 malicious labels group into a few behaviours. Map mitigations to the
behaviour, not the malware name — that is cleaner and more defensible.

---

## A. Reconnaissance — `PartOfAHorizontalPortScan`
**What it is:** the infected device scans many hosts for open ports/services to find new
victims (horizontal = same port across many IPs). Usually the *first* stage of an IoT
botnet spreading.

**MITRE ATT&CK:** T1046 — Network Service Discovery *(verified)*.

**Mitigations (verify IDs, then rewrite):**
- Network segmentation / VLANs so a compromised IoT device cannot scan the wider network.
- Firewall egress + east-west ACLs; deny device-to-device traffic that isn't required.
- IDS/IPS scan-detection and rate-limiting (e.g. Zeek/Suricata scan signatures).
- Frameworks: MITRE Mitigation *Network Segmentation (M1030)*; NIST CSF **PR.AC**/**PR.PT**;
  CIS Controls v8 **4** (secure config), **12** (network infrastructure), **13** (network
  monitoring).

## B. Command & Control — `C&C`, `C&C-HeartBeat`, `C&C-Torii`, `C&C-Mirai`
**What it is:** the device talks to an attacker-controlled server — receiving commands or
sending periodic "heartbeat" check-ins. Often over standard protocols or IRC to blend in.

**MITRE ATT&CK:** T1071 — Application Layer Protocol *(verified)*; consider also
T1571 — Non-Standard Port, and T1095 — Non-Application Layer Protocol (IRC-based C2).
*(verify the latter two)*

**Mitigations:**
- Egress filtering / default-deny outbound; allow only required destinations.
- DNS filtering and threat-intel blocklists to block known C2 domains/IPs.
- Detect beaconing (regular heartbeat intervals) in network monitoring.
- Frameworks: MITRE *Filter Network Traffic (M1037)*, *Network Intrusion Prevention (M1031)*;
  NIST CSF **DE.CM**, **PR.DS**; CIS **9** (email/web protections), **13**.

## C. Payload / Tool delivery — `C&C-FileDownload`, `FileDownload`, `C&C-HeartBeat-FileDownload`
**What it is:** the device downloads a binary/second-stage payload (e.g. the bot updating
itself or pulling DDoS modules).

**MITRE ATT&CK:** T1105 — Ingress Tool Transfer *(verify)*.

**Mitigations:**
- Block outbound to untrusted hosts; restrict which sources a device may fetch from.
- Network IPS to inspect/deny known-malicious payload transfers.
- Application allow-listing on the device where feasible.
- Frameworks: MITRE *Network Intrusion Prevention (M1031)*; NIST CSF **PR.DS**/**DE.CM**;
  CIS **10** (malware defences).

## D. Denial of Service — `DDoS`
**What it is:** the device participates in flooding a target (the classic IoT-botnet use,
e.g. Mirai). It may be the *source* of attack traffic, not the victim.

**MITRE ATT&CK:** T1498 — Network Denial of Service *(verified)*; T1499 — Endpoint Denial
of Service *(verified)*.

**Mitigations:**
- Upstream DDoS protection / traffic scrubbing for the *targeted* service.
- Egress rate-limiting and anti-spoofing (BCP38) so the device can't be used as a bot.
- Detect abnormal outbound volume per device.
- Frameworks: MITRE *Filter Network Traffic (M1037)*; NIST CSF **PR.PT**/**DE.AE**;
  CIS **13**.

## E. Exploitation / Intrusion — `Attack`
**What it is:** active attempts against another host — telnet/SSH brute force, command
injection, exploiting a vulnerable service. How IoT botnets recruit new devices.

**MITRE ATT&CK:** T1110 — Brute Force; T1190 — Exploit Public-Facing Application;
T1059 — Command and Scripting Interpreter *(verify all three)*.

**Mitigations:**
- Remove default credentials; enforce strong unique passwords; disable Telnet (use SSH).
- Patch/update firmware; close unused services.
- Input validation on device web interfaces; account lockout/rate-limit on logins.
- Frameworks: MITRE *Password Policies (M1027)*, *Update Software (M1051)*; NIST CSF
  **PR.AC**/**PR.IP**; CIS **4**, **5** (account management); IoT-specific **NIST IR 8259**.

## F. Botnet malware umbrella — `Okiru`, `C&C-Mirai` (and the capture-level malware: Mirai, Torii, Kenjiro, Hakai, IRCBot, Muhstik, Hide-and-Seek, Gagfyt)
**What it is:** these are full botnets that combine the behaviours above (scan → brute-force
→ download payload → C2 → DDoS). Map them to the *combination* of A–E rather than a single
technique. Okiru/Mirai variants especially: Telnet brute force (E), scanning (A), C2 (B), DDoS (D).

**Cross-cutting IoT hardening (cite for the whole section):** change default creds,
disable Telnet/UPnP, segment IoT onto their own VLAN, keep firmware patched, monitor
egress. Frameworks: **NIST IR 8259** (IoT device cybersecurity capabilities), **ENISA
Baseline Security Recommendations for IoT**, **OWASP IoT Top 10**.

---

## Sources (verify and cite properly in Harvard for your report)
- IoT-23 dataset & label definitions — Stratosphere Laboratory: https://www.stratosphereips.org/datasets-iot23
- MITRE ATT&CK technique pages (look up each Txxxx and its listed Mitigations): https://attack.mitre.org/techniques/enterprise/
- NIST Cybersecurity Framework; NIST IR 8259 (IoT); CIS Critical Security Controls v8; OWASP IoT Top 10; ENISA IoT guidance.

## Your write-up task (RQ3)
For each attack type your EDA actually found: 1-2 sentences on what it is, the ATT&CK
technique (with verified ID), and 2-3 concrete mitigations tied to a named framework.
Keep it in your own words. This directly answers RQ3.
