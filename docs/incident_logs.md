# Incident Response Log – Compromised Office 365 Credentials & Internal Portal Access

**Incident ID:** IR-2025-001  
**Incident Category:** Credential Compromise & Internal Resource Breach  
**Status:** Ongoing Investigation  
**Reported Date:** 2025-08-07  
**Detected By:** SOC Analyst via Phishing Alert  

---

## 📝 Executive Summary
An employee received a targeted phishing email containing a malicious link to a spoofed Office 365 login page. The attacker successfully harvested the victim’s credentials. Using these credentials, the attacker accessed the victim’s Office 365 mailbox and discovered internal communication that contained the link to the company’s internal portal. The same stolen credentials granted them access to this internal system, escalating the compromise.

This document serves as the running **Incident Response (IR) log**, capturing investigative actions, findings, and response measures.

---

## 📅 Timeline of Events

| Date & Time (IST) | Event | Details |
|-------------------|-------|---------|
| 2025-08-07 09:30  | Phishing Email Delivered | User reports suspicious email to SOC. Email contains link to spoofed Office 365 login page. |
| 2025-08-07 09:35  | Email Analysis Initiated | Email headers pulled from O365 security portal. Suspicious domain identified: `login-office365-secure[.]com`. |
| 2025-08-07 09:45  | Phishing Link Investigation | SOC sandbox analysis confirms phishing page mimics Microsoft login and exfiltrates credentials to attacker's server. |
| 2025-08-07 10:00  | Credential Compromise Confirmed | Review of O365 sign-in logs shows successful login from unusual IP in another country (Nigeria). |
| 2025-08-07 10:10  | Attacker Mailbox Activity | Analysis shows attacker browsing victim’s mailbox. Multiple internal threads accessed, including one with internal portal URL. |
| 2025-08-07 10:20  | Internal Portal Access | Logs confirm attacker logged into internal portal using same stolen O365 credentials. |
| 2025-08-07 10:30  | IR Escalation | Incident escalated to Tier-3 and Incident Response Team. Decision made to reset victim credentials across all systems. |
| 2025-08-07 11:00  | Containment Measures | O365 account locked, internal portal session terminated, and MFA enforced. |
| 2025-08-07 12:00  | Forensic Data Preservation | All related logs, phishing email, and malicious artifacts preserved for further analysis. |

---

## 🔍 Detailed Analysis

### 1. Phishing Email Examination
- **Sender:** `it-support@secure-office365[.]com`
- **Return-Path:** Different from sender, indicative of spoofing.
- **SPF/DKIM/DMARC:** Failed SPF check.
- **URL in Email:** `https://login-office365-secure[.]com/`
- **Hosting Info:** Hosted on compromised web server in Eastern Europe.

**Observation:** Highly targeted phishing, using branding identical to Microsoft’s O365 login page.

---

### 2. Credential Harvesting
- Attacker’s phishing page used HTTPS with a valid-looking certificate (Let's Encrypt) to increase credibility.
- JavaScript captured credentials and sent them via HTTP POST request to `attacker-collect[.]net/api/store_creds`.
- Victim entered their real credentials thinking it was a legitimate login.

---

### 3. Unauthorized Office 365 Access
- Sign-in logs show:
  - **Source IP:** `102.89.xxx.xxx` (Nigeria)
  - **Device:** Unknown browser on Windows.
  - **Authentication:** Password only (no MFA).
- Attacker accessed mailbox folders:
  - Inbox
  - Sent Items
  - Important flagged emails
- Found an internal IT bulletin containing internal portal link.

---

### 4. Internal Portal Compromise
- Attacker accessed internal portal: `https://intranet.companyname.com`
- Same O365 credentials worked due to single sign-on (SSO) configuration.
- Activity:
  - Viewed internal HR documents.
  - Accessed project management dashboard.
  - Downloaded one internal contact directory CSV.

---

## 🚨 Impact Assessment
- **Compromised Assets:**
  - One O365 account
  - Internal portal access
- **Data Exfiltrated:**
  - Possible exposure of contact directory (names, job titles, email addresses)
  - No confirmed access to sensitive financial or customer PII yet
- **Business Impact:**
  - Risk of further spear-phishing using internal contacts
  - Potential lateral movement within network

---

## 🛡 Containment & Mitigation Steps
1. Locked O365 account and forced global logout.
2. Reset credentials in O365 and internal portal.
3. Enforced MFA on all accounts.
4. Blocked attacker IP ranges in firewall and O365 conditional access policy.
5. Implemented rule to detect & quarantine emails from lookalike domains.
6. Notified all employees to be alert for internal phishing attempts.

---

## 📌 Next Steps
- Perform full mailbox content review for other compromised communications.
- Review internal portal logs for further attacker activity.
- Conduct company-wide phishing awareness refresher training.
- Evaluate conditional access policies to limit login locations.
- Enhance SIEM alerting for anomalous logins and SSO access.

---

**Prepared By:** SOC Analyst – Yug Shah  
**Date:** 2025-08-09  
**Status:** 🔴 Active – Monitoring in progress

