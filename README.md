# 🛡️ Wazuh SIEM / SOC — Complete Implementation Lab

> A practical, end-to-end Wazuh SIEM/SOC implementation covering deployment, endpoint onboarding, log collection, detection engineering, cloud security monitoring, vulnerability management, investigation, response, and troubleshooting.

---

## 🎯 Project Overview

This project provides a hands-on Wazuh SIEM/SOC implementation designed to build practical security monitoring and SOC investigation capabilities.

The lab covers the complete security monitoring lifecycle:

```text
Data Sources
     ↓
Collection
     ↓
Ingestion
     ↓
Decoding
     ↓
Detection
     ↓
Alert
     ↓
Investigation
     ↓
Response
     ↓
Validation
     ↓
Troubleshooting
```

The objective is not simply to install Wazuh, but to understand how security telemetry moves through the platform and how a SOC analyst uses that telemetry for detection and investigation.

---

## 🏗️ Wazuh Architecture

```text
                         ┌──────────────────────┐
                         │   Wazuh Dashboard    │
                         │ Investigation / SOC  │
                         └──────────┬───────────┘
                                    │
                         ┌──────────▼───────────┐
                         │    Wazuh Server      │
                         │ Manager + Filebeat   │
                         │ Rules + Decoders     │
                         └──────────┬───────────┘
                                    │
                         ┌──────────▼───────────┐
                         │    Wazuh Indexer     │
                         │ Events / Alerts      │
                         └──────────────────────┘

       ┌─────────────┬─────────────┬─────────────┬──────────────┐
       │             │             │             │              │
    Windows       Linux       Firewall/IDS      Cloud       Applications
     Agent        Agent         Syslog           APIs            Logs
```

---

## 🧪 Lab Components

| Component | Example |
|---|---|
| Wazuh Server | Ubuntu 22.04 / 24.04 |
| Windows Endpoint | Windows 10 / 11 |
| Linux Endpoint | Ubuntu Server |
| Network Devices | pfSense / FortiGate / SonicWall |
| Cloud | AWS / Azure / GCP |
| Application | Nginx / Custom Application |
| Container | Docker |
| Detection | Custom Wazuh Rules & Decoders |

---

## 🛠️ Implementation Areas

### 🖥️ Wazuh Platform

- Wazuh Indexer
- Wazuh Manager
- Wazuh Dashboard
- Service validation
- Agent enrollment
- Configuration management

### 🪟 Windows Security Monitoring

- Windows Security Events
- System Events
- Application Events
- PowerShell logging
- Sysmon
- Process activity
- Authentication monitoring
- Suspicious execution

### 🐧 Linux Security Monitoring

- Authentication logs
- SSH activity
- Syslog
- Sudo activity
- Root logins
- User creation
- Persistence activity
- Application logs

### 🌐 Network Security

- Firewall logs
- Syslog collection
- VPN activity
- Administrative logins
- Firewall denies
- Configuration changes
- Suspicious outbound connections

### ☁️ Cloud Security

#### AWS

- CloudTrail
- GuardDuty
- VPC activity
- WAF
- S3-based log collection
- IAM activity

#### Azure / Entra ID

- Authentication
- Failed logins
- MFA activity
- User creation
- Role assignments
- Conditional Access

#### Microsoft 365

- Audit activity
- Exchange
- SharePoint
- OneDrive
- Teams
- Entra activity

#### Google Cloud

- Audit Logs
- IAM activity
- VM activity
- Network activity
- Logging
- Pub/Sub integration

#### GitHub

- Authentication
- Repository access
- Permission changes
- Organization changes
- PAT/token activity
- Repository security events

---

## 🔍 Detection Engineering

The project includes practical detection engineering using:

```text
Raw Logs
   ↓
Pre-decoding
   ↓
Decoder
   ↓
Structured Fields
   ↓
Detection Rule
   ↓
Severity
   ↓
Alert
```

### 🧩 Custom Decoders

Custom decoders are implemented under:

```text
/var/ossec/etc/decoders/
```

### 🚨 Custom Rules

Custom rules are implemented under:

```text
/var/ossec/etc/rules/local_rules.xml
```

Custom rule IDs:

```text
100000–120000
```

### 🧪 Rule Testing

Rules and decoders are tested using:

```bash
sudo /var/ossec/bin/wazuh-logtest
```

---

## 🎯 SOC Detection Use Cases

The lab covers detection scenarios including:

### 🔐 Authentication

- Multiple failed logins
- Brute-force activity
- Successful login after failures
- Invalid users
- Privileged logins
- New accounts
- Account disablement

### 🪟 Windows

- PowerShell execution
- Encoded PowerShell
- Suspicious process trees
- New services
- Scheduled tasks
- Registry modifications
- LSASS access
- Credential-dumping indicators
- Malware execution

### 🐧 Linux

- SSH brute force
- Root login
- Sudo abuse
- New users
- Cron modification
- Suspicious shells
- Binary execution
- Persistence

### 🌐 Network

- Port scanning
- Firewall denies
- VPN logins
- Administrative logins
- Configuration changes
- Suspicious outbound connections

### ☁️ Cloud

- Root/admin login
- MFA disabled
- IAM privilege escalation
- Access-key creation
- Security-group modifications
- CloudTrail disabled
- Suspicious API activity

---

## 🧬 Security Controls

### 📁 File Integrity Monitoring

Monitor important directories for:

- File creation
- File modification
- File deletion

Example monitored paths:

```text
/etc
/var/www
```

### 🩺 Vulnerability Detection

Wazuh endpoint inventory is used to identify:

- Vulnerable packages
- CVEs
- Installed versions
- Severity
- Remediation information

### 📋 Security Configuration Assessment

SCA provides:

- Passed checks
- Failed checks
- Security scores
- Policies
- Recommendations

### 🐳 Docker Monitoring

Monitor container lifecycle activity such as:

```text
Container creation
Container pause
Container resume
Container stop
Container removal
```

---

## ⚡ Active Response

The lab also covers automated response workflows:

```text
Detection
   ↓
Rule ID / Severity
   ↓
Active Response
   ↓
Endpoint Action
```

Possible actions include:

- Block IP
- Disable account
- Kill process
- Delete/quarantine file
- Restart service

> ⚠️ Active Response should be thoroughly tested in a lab before enabling automated blocking in production.

---

## 🔎 SOC Investigation Methodology

For every alert, investigate:

```text
1. What happened?
2. Which user?
3. Which endpoint?
4. Source IP?
5. Destination IP?
6. Process?
7. Parent process?
8. Command line?
9. Timestamp?
10. What happened before?
11. What happened after?
12. Is the activity expected?
13. Is there evidence of persistence?
14. Is lateral movement possible?
15. What containment is required?
```

The investigation focuses on building an evidence-based timeline rather than treating an individual alert in isolation.

---

## 🛠️ Troubleshooting Method

The complete troubleshooting path is:

```text
SOURCE
   ↓
NETWORK
   ↓
AGENT
   ↓
MANAGER
   ↓
INGESTION
   ↓
DECODER
   ↓
RULE
   ↓
ALERT
   ↓
INDEXER
   ↓
DASHBOARD
```

Useful validation commands include:

```bash
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-agent
sudo tail -f /var/ossec/logs/ossec.log
sudo tail -f /var/ossec/logs/alerts/alerts.json
sudo ss -lntup
sudo /var/ossec/bin/wazuh-logtest
```

---

## 🔐 Security & Repository Protection

Never commit:

```text
Passwords
Private keys
Cloud credentials
API tokens
Client secrets
.env files
Customer logs
Personal information
Sensitive production IPs
Real security incidents
```

Use placeholders:

```text
<WAZUH_SERVER_IP>
<AGENT_IP>
<AWS_ACCOUNT_ID>
<BUCKET_NAME>
<TENANT_ID>
<CLIENT_ID>
<CLIENT_SECRET>
```

---

## ✅ Final Validation

The lab should validate:

```text
[ ] Wazuh Indexer
[ ] Wazuh Manager
[ ] Wazuh Dashboard
[ ] Windows Agent
[ ] Linux Agent
[ ] Windows Security Logs
[ ] Sysmon
[ ] Linux SSH Logs
[ ] Application Logs
[ ] Firewall Logs
[ ] AWS
[ ] Azure
[ ] Microsoft 365
[ ] GCP
[ ] GitHub
[ ] FIM
[ ] Vulnerability Detection
[ ] SCA
[ ] Docker Monitoring
[ ] Custom Decoder
[ ] Custom Rule
[ ] wazuh-logtest
[ ] Active Response
[ ] SOC Detection Use Cases
[ ] Troubleshooting
[ ] Backups
[ ] Secrets excluded from Git
```

---

## 🔄 Complete SOC Pipeline

```text
                    DATA SOURCES
                         │
          ┌──────────────┼──────────────┐
          │              │              │
       Endpoint        Network         Cloud
          │              │              │
      Wazuh Agent      Syslog           API
          │              │              │
          └──────────────┼──────────────┘
                         ↓
                  WAZUH MANAGER
                         ↓
                     DECODERS
                         ↓
                       RULES
                         ↓
                      ALERTS
                         ↓
                     INDEXER
                         ↓
                    DASHBOARD
                         ↓
                   SOC ANALYSIS
                         ↓
                INCIDENT RESPONSE
                         ↓
                  ACTIVE RESPONSE
```

---

## 🧠🔥 Project Goal

The goal of this project is to build practical Wazuh SIEM/SOC capabilities and understand the complete security monitoring lifecycle.

> **The lab is complete when you can Install → Enroll → Collect → Decode → Detect → Investigate → Tune → Respond → Validate → Troubleshoot — and explain exactly where each step occurs.**

---

## 📚 Project Documentation

Detailed implementation and investigation procedures are maintained within the Wazuh project documentation, covering the individual installation, integration, detection, investigation, response, and troubleshooting phases.

---

## ⚠️ Disclaimer

This project is intended for **educational, lab, and authorized security testing purposes only**.

Do not use these configurations or testing techniques against systems, networks, cloud environments, applications, or accounts without appropriate authorization.
