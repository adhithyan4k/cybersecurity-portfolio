# SIEM Home Lab — Splunk Threat Detection

**Analyst:** Adhithyan AK
**Date:** May 2, 2026
**Tool:** Splunk Enterprise 10.2.3
**OS:** Windows 11

---

## Objective
Build a fully functional SIEM home lab to simulate
real SOC operations — ingest Windows logs, create
detection rules, investigate security events, and
build a monitoring dashboard.

---

## Environment Setup

| Component | Details |
|-----------|---------|
| SIEM Tool | Splunk Enterprise 10.2.3 |
| OS | Windows 11 |
| Log Sources | Windows Security, Application, System |
| Total Events | 103,847+ events indexed |
| Security Events | 6,370 events |
| Access | http://localhost:8000 |

---

## Step 1: Log Ingestion

**What I did:**
- Installed Splunk Enterprise 10.2.3 on Windows
- Configured Local Event Log monitoring
- Added Security, Application, System logs
- Verified 103,847+ events flowing into Splunk

**SPL Query used:**
index=main sourcetype="WinEventLog:Security"
**Result:** 6,370 security events confirmed

---

## Step 2: Simulating Brute Force Attack

**What I did:**
1. Enabled Windows Audit Policy: auditpol /set /subcategory:"Logon"
/failure:enable /success:enable
2. Simulated failed logins: runas /user:fakeuser123 cmd
3. 3. Ran 5+ times to simulate brute force

**Result:** 13 failed login events (EventCode 4625)
detected with attacker accounts identified:
- fakeuser123
- vaisav
- INIHDA$

---

## Step 3: Detection Query

**Brute Force SPL:**
index=main sourcetype="WinEventLog:Security"
EventCode=4625
| stats count by Account_Name
| where count > 3
**What this does:**
- Searches Windows Security logs
- Filters failed login events (4625)
- Groups by account name
- Flags accounts with 3+ failures
- Maps to MITRE ATT&CK T1110

---

## Step 4: Alert Created

**Alert: Brute Force Login Detection**

| Setting | Value |
|---------|-------|
| Type | Scheduled Hourly |
| Trigger | Results greater than 0 |
| Severity | HIGH |
| Action | Add to Triggered Alerts |
| MITRE | T1110 Brute Force |

---

## Step 5: SOC Dashboard Built

**Dashboard: SOC Security Monitoring Dashboard**

**Panel 1 - Security Events by Type:**
index=main sourcetype="WinEventLog:Security"
| stats count by EventCode
| sort -count
Visualization: Column Chart
**Panel 2 - Failed Login Timeline:**
index=main
sourcetype="wineventlog:security"
Eventcode=4625
| timechart count span=1h
Visualization: Line Chart
Spike visible at 10PM May 2, 2026 —
exactly when brute force was simulated!

---

## Key Results

| Finding | Value |
|---------|-------|
| Total events ingested | 103,847+ |
| Security events | 6,370 |
| Failed logins detected | 13 |
| Alert created | Brute Force Detection |
| Dashboard panels | 2 |
| Attack simulation | Successful |

---

## MITRE ATT&CK Mapping

| Technique | ID | Detected By |
|-----------|-----|-------------|
| Brute Force | T1110 | EventCode 4625 |
| Valid Accounts | T1078 | EventCode 4624 |
| Account Discovery | T1087 | EventCode 4798 |

---

## Windows Event Codes Reference

| EventCode | Meaning |
|-----------|---------|
| 4625 | Failed Login — Brute force |
| 4624 | Successful Login |
| 4648 | Explicit Credentials |
| 4798 | User Account Query |
| 4672 | Special Privileges |

---

## SOC Workflow Practiced
---

## Conclusion
Successfully built a functional SIEM environment
simulating real SOC operations. Detected real
brute force events, created automated alerts,
and built monitoring dashboard aligned with
real SOC L1 analyst workflows.

---

## Screenshots
See /Screenshots folder for all evidence

