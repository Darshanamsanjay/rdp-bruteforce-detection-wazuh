# 🛡️ Rdp-bruteforce-detection-wazuh

## 📌 Project Overview
This project demonstrates a **Mini Security Operations Center (SOC) Lab** built using Wazuh SIEM, Windows 10 Pro, and Kali Linux.

The objective was to simulate real-world cyber attacks and detect them using SIEM-based monitoring and correlation rules.

---

## 🧱 Lab Architecture

- 🖥️ Windows 10 Pro (Victim Machine)
- 🐧 Kali Linux (Attacker Machine)
- 🛡️ Wazuh SIEM (Ubuntu Server)


---

## ⚙️ Tools & Technologies

- Wazuh SIEM
- Kali Linux
- Windows 10 Pro
- RDP (Remote Desktop Protocol)
- Bash / Command Line
- VirtualBox / VMware

---

## 🔥 Attack Simulation

- Performed RDP brute-force attack using:
```bash
xfreerdp /v:<target-ip> /u:admin /p:wrongpass +auth-only
```

## Log Analysis
Monitored Windows Security Logs
Detected:
Event ID 4625 → Failed login
Event ID 4624 → Successful login

🚨 Detection Rules
🔹 Failed Login Detection

```bash
<rule id="100001" level="8">
  <if_group>windows</if_group>
  <field name="win.system.eventID">4625</field>
  <description>Failed login detected</description>
</rule>
```

🔹 Brute Force Detection
```bash
<rule id="100100" level="12" frequency="5" timeframe="60">
  <if_matched_sid>100001</if_matched_sid>
  <description>RDP Brute Force Attack Detected</description>
</rule>
```

## 📈 Results
Detected multiple failed login attempts
Identified attacker IP from Kali Linux
Observed account lockout after repeated failures
Triggered alerts in Wazuh dashboard

## 🧠 MITRE ATT&CK Mapping
Technique: T1110 – Brute Force
Tactic: Credential Access

## 🎯 Key Learnings
SIEM log ingestion and analysis
Windows security event monitoring
Detection rule creation
Brute-force attack behavior analysis


