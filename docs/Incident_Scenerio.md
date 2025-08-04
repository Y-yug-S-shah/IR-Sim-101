# 🧠 IR Sim 101 – Incident Scenario

## 🎯 Overview

This simulation walks through a realistic cloud-to-internal attack path often seen in modern organizations. It’s designed for beginner to intermediate blue teamers and threat intel learners working on low-resource systems.

---

## 🧩 Attack Narrative

A non-admin employee at **AcmeCorp**, working in the Finance department, receives a phishing email that looks like a legitimate Microsoft 365 security alert. The email urges the user to log in immediately due to a suspicious sign-in attempt.

The victim clicks the embedded link and unknowingly submits their **Office 365** credentials to a fake login page controlled by the attacker.

---

## 🔓 Stage 1: Initial Access – Credential Harvesting

- The attacker successfully captures the user's **email and password**.
- These are **cloud-only credentials**, not yet proven valid elsewhere.

---

## 🔍 Stage 2: Cloud Access and Recon

- The attacker logs into the user's real Office 365 account using the stolen credentials (no MFA in place).
- From the inbox, they:
  - Access sensitive financial emails and files.
  - Identify an internal AcmeCorp **portal login URL** shared in previous conversations with HR and IT.

---

## 💥 Stage 3: Internal Pivot – Portal Reuse

- The attacker attempts to log in to the internal portal using the **same harvested credentials**.
- Due to **poor credential hygiene and reuse**, the portal accepts the same username and password.
- The attacker is now inside AcmeCorp’s internal web portal.

---

## 🛠 Stage 4: Simulated Post-Access Activity

To simulate real-world attack behaviors, we demonstrate:

- PowerShell command usage mimicking internal recon or credential access (simulated locally).
- Use of example TTPs like:
  - `T1059.001` – PowerShell execution
  - `T1110.001` – Password spraying (simulated via reuse)
  - `T1087` – User account discovery
- Local event log or file-based artifacts generated to simulate logs an analyst might review.

---

## 📚 Learning Goals

- Understand the risk of **cloud credential compromise**.
- Simulate realistic cloud-to-internal pivot paths.
- Learn to detect artifacts from credential harvesting and PowerShell misuse.
- Practice mapping TTPs using MITRE ATT&CK (plain text).

---

## ⚠️ Disclaimer

This is a simulated scenario intended for educational use only.  
All activities are conducted in isolated, controlled environments using non-malicious code.  
Any resemblance to real companies, systems, or data is purely coincidental.

---

