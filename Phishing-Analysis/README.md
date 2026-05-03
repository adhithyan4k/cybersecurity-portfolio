# Phishing Email Analysis & Threat Investigation

**Analyst:** Adhithyan A K
**Date:** April 30, 2026
**Severity:** HIGH
**Tools:** VirusTotal | URLScan.io | AbuseIPDB | MXToolbox | OpenPhish

---

## Objective
Identify, analyze, and document 3 real-world active
phishing campaigns using SOC analyst tools.

---

## Tools Used
| Tool | Purpose |
|------|---------|
| OpenPhish | Live phishing URL feed |
| VirusTotal | URL/IP malware scanning |
| URLScan.io | Website behavior analysis |
| AbuseIPDB | IP reputation checking |
| MXToolbox | Email header analysis |

---

## Methodology
1. Collected active phishing URLs from OpenPhish
2. Analyzed each URL on VirusTotal
3. Submitted to URLScan.io for behavior analysis
4. Checked attacker IPs on AbuseIPDB
5. Analyzed phishing email headers on MXToolbox
6. Mapped findings to MITRE ATT&CK
7. Documented IOCs and produced incident report

---

## Sample 1 — Microsoft Phishing

**URL:** verificarmicuentaa-microsoft2o26.zya.me

**What I found:**
- Typosquatting — microsoft2o26 replaces O with 0
- Fake Microsoft login page in Spanish
- Password-input field = credential harvesting
- Domain created March 27, 2026

**VirusTotal:** 8/92 engines flagged
ADMINUSLabs, BitDefender, CyRadar, Fortinet,
G-Data, Kaspersky, LevelBlue, Webroot

**URLScan:** Potentially Malicious
- Targeting Microsoft Consumer
- Fake login page (Inicio sesion) visible

**AbuseIPDB — 185.27.134.135:**
- ISP: I FastNet LTD, London UK
- Usage: Data Center (RED FLAG)

**MITRE ATT&CK:**
- T1566.001 Spearphishing Link
- T1036 Masquerading
- T1598 Phishing for Information

---

## Sample 2 — Google Phishing

**URL:** google-sign-in.github.io/ooh

**What I found:**
- Attacker abusing GitHub Pages to host phishing
- Fake Google Sign-In page
- GitHub trusted domain bypasses URL filters
- Google SafeBrowsing itself flagged as Malicious

**VirusTotal:** 17/92 engines flagged
**URLScan:** Malicious Activity — targeting Google

**AbuseIPDB — 185.199.108.153:**
- ISP: GitHub Inc, San Francisco USA
- Abuse: 35% confidence, 10 reports

**MITRE ATT&CK:**
- T1566.001 Spearphishing Link
- T1583.006 Web Services Abuse (GitHub Pages)

---

## Sample 3 — Netflix Phishing

**URL:** shekharscript.github.io/Netflix-clone

**What I found:**
- Same GitHub Pages abuse as Sample 2
- Convincing Netflix India homepage replica
- Highest detection rate of all 3 samples
- Scanned 19 times on URLScan

**VirusTotal:** 19/92 engines flagged (highest)
**URLScan:** Malicious — targeting Netflix Online

**AbuseIPDB — 185.199.110.153:**
- ISP: GitHub Inc, San Francisco USA
- Abuse: 39% confidence, 227 reports

**MITRE ATT&CK:**
- T1566.001 Spearphishing Link
- T1583.006 Web Services Abuse

---

## Email Header Analysis — MXToolbox

**Subject:** Your Google Account Has Been
Compromised - Immediate Action Required

| Header | Value | Finding |
|--------|-------|---------|
| From | security-alert@g00gle-accounts.com | SPOOFED |
| Reply-To | recover@protonmail.com | MISMATCH |
| Return-Path | bounce@phishing-server.xyz | MISMATCH |
| X-Mailer | PhishMailer 3.0 | Phishing tool |
| SPF | FAIL | Not authorized |
| DKIM | FAIL | Invalid signature |
| DMARC | FAIL | No policy |

---

## Consolidated IOCs

| Type | Indicator | Action |
|------|-----------|--------|
| URL | verificarmicuentaa-microsoft2o26.zya.me | BLOCK |
| URL | google-sign-in.github.io/ooh | BLOCK |
| URL | shekharscript.github.io/Netflix-clone | BLOCK |
| IP | 185.27.134.135 | BLOCK |
| IP | 185.199.108.153 | MONITOR |
| IP | 185.199.110.153 | MONITOR |

---

## Key Finding
Samples 2 and 3 abuse GitHub Pages to host
phishing — advanced evasion bypassing URL filters.

---

## Recommendations
1. Block all IOCs at email gateway and web proxy
2. Report GitHub repos to security@github.com
3. Implement DMARC/SPF/DKIM authentication
4. User awareness training on typosquatting
5. Add IOCs to SIEM threat intelligence feeds

---

## Screenshots
See /screenshots folder for all evidence
