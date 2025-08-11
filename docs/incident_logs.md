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

| Date & Time (IST)       | Event                                                                                                                                  |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **04 Aug 2025 – 09:15** | Attacker sends phishing email to targeted employee’s corporate mailbox (Office 365). Email contains malicious link to fake login page. |
| **04 Aug 2025 – 09:27** | Victim clicks the link and enters credentials into attacker-controlled phishing site.                                                  |
| **04 Aug 2025 – 09:29** | Attacker receives harvested Office 365 credentials via phishing backend.                                                               |
| **04 Aug 2025 – 09:41** | Attacker logs into Office 365 web portal successfully from an IP located outside the usual geolocation for the account.                |
| **04 Aug 2025 – 09:55** | While browsing the victim’s mailbox, attacker discovers an **internal portal link** in older internal communications.                  |
| **04 Aug 2025 – 10:07** | Attacker attempts login to the internal portal using the same stolen Office 365 credentials — login is successful.                     |
| **04 Aug 2025 – 10:15** | From the internal portal, attacker identifies a feature allowing authenticated users to trigger PowerShell-based automation scripts.   |
| **04 Aug 2025 – 10:21** | Attacker executes malicious PowerShell commands to enumerate network shares and extract basic system information.                      |
| **04 Aug 2025 – 10:27** | Attacker uploads a second-stage PowerShell script for credential harvesting and lateral movement preparation.                          |
| **04 Aug 2025 – 10:39** | Unusual PowerShell activity triggers security monitoring alerts in SOC dashboard.                                                      |
| **04 Aug 2025 – 10:45** | SOC analyst reviews alert, correlates with Office 365 login logs, and raises an incident ticket.                                       |
| **04 Aug 2025 – 11:02** | Incident Response team initiates account suspension and network isolation for affected systems.                                        |
| **04 Aug 2025 – 11:27** | Forensic acquisition begins for compromised endpoint and Office 365 mailbox logs.                                                      |
| **04 Aug 2025 – 12:15** | IOC extraction and network traffic analysis confirm malicious activity originated from external attacker infrastructure.               |
| **04 Aug 2025 – 13:00** | Containment completed, incident moved to eradication & recovery phase.                                                                 |
| **04 Aug 2025 – 14:30** | Security policy updates and MFA enforcement rolled out to all users.                                                                   |
| **04 Aug 2025 – 16:00** | Incident post-mortem conducted and documented in final report.                                                                         |


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

## Containment & Mitigation Steps
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

