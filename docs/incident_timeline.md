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
