# OWASP Juice Shop — Penetration Testing Report

**Prepared by:** Adhithyan AK  
**Date:** May 2026  
**Target:** localhost:3000 (VirtualBox)  
**Tools Used:** Burp Suite, Kali Linux  

## Vulnerabilities Identified 

1. SQL Injection (Critical) — Admin account takeover via OR 1=1
2. Cross-Site Scripting XSS (Critical) — Script injection in search bar
3. Sensitive Data Exposure (Critical) — /ftp/acquisitions.md accessible
4. Broken Access Control (Critical) — /administration panel exposed
5. Security Misconfiguration (High) — Swagger API docs publicly visible

## Full Report
See attached PDF report for complete documentation with screenshots,
impact analysis, and remediation steps.
