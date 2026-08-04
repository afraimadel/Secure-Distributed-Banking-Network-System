# 🛡️ SOC Implementation — Secure Banking Network (Blue Team / SIEM)

This repository documents my **individual contribution as SOC (Security Operations Center) engineer** within a larger graduation team project — *"Simulation of a Secure and Distributed Banking Network System"* — Sohag University, Faculty of Computers and Artificial Intelligence, Network Department (2025–2026).

> ⚠️ **Scope note:** The full project (network design, routing/switching, FortiGate firewalls, Linux server infrastructure, VoIP) was built by a team. **My role was the SOC / Blue Team component** — deploying and operating the SIEM, managing monitored endpoints, and handling detection & response. This repo focuses specifically on that work.

---

## 🎯 My Role

As the SOC engineer on the team, my responsibility was to protect the simulated banking infrastructure through **continuous monitoring, threat detection, and incident response**, acting as the Blue Team of the project. This involved deploying **Wazuh** (SIEM) to collect and analyze security events from all critical banking servers, alongside **Zabbix** for infrastructure health monitoring.

---

## 🧩 What I Built

### 1. Wazuh SIEM Deployment
- **All-in-One deployment** on an Ubuntu VM (`192.168.206.130`)
- Full install pipeline: system update → download installation script & `config.yml` → run installer → verify services → access dashboard
- Opened and configured required firewall ports for agent ↔ manager communication
- Documented daily management commands and a troubleshooting reference

### 2. Agent Management
- Deployed and registered Wazuh agents across both **Linux and Windows** endpoints in the banking network
- Used the Agent Manager to add, monitor, and authenticate connected agents
- Verified agent status (ID, IP, OS, connection state) for every monitored server (Admin, DNS, DHCP, Mail, SFTP, Backup)

### 3. Log Collection & Monitoring
- Centralized log collection from all endpoints into a single Wazuh dashboard
- Monitored system activity, application events, and user actions across the infrastructure

### 4. Threat Detection & Alerting
- Configured and reviewed **real-time security events**: suspicious activity, failed logins, unauthorized access attempts
- Investigated **authentication failure** patterns as indicators of potential attacks
- Used **filtering** (by severity, rule group, event type) to speed up alert triage
- Reviewed severity-classified **security alerts** with rule ID, timestamp, and full event description

### 5. Active Response (Automated Mitigation)
- Configured **Active Response rules** — e.g., automatically blocking an IP after repeated failed login attempts
- Verified live Active Response execution (automatic IP blocking / malicious process termination)

### 6. Vulnerability Assessment
- Ran vulnerability scans across monitored endpoints to identify outdated/vulnerable packages and misconfigurations
- Prioritized findings by severity for remediation

### 7. Infrastructure Health Monitoring (Zabbix)
- Deployed **Zabbix 7.0** on Ubuntu 22.04 (repo setup, MySQL backend, schema import, Apache/PHP config)
- Monitored device/service availability, HSRP state changes, interface failures, and CPU/memory thresholds with real-time alerting

---

## 🛠️ Tools Used

| Category | Tool |
|---|---|
| SIEM | **Wazuh** (Manager + Agents, Linux & Windows) |
| Infrastructure Monitoring | **Zabbix 7.0** |
| OS | Ubuntu Server (20.04/22.04) |
| Virtualization | VMware Workstation |
| Dashboard/Access | Cockpit (system-level monitoring) |

---

## 📂 Repository Structure

```
├── docs/
│   └── SOC-Documentation.pdf            # My write-up: Wazuh + Zabbix deployment & results
├── wazuh/
│   ├── config.yml                       # Wazuh all-in-one install config
│   ├── install-notes.md                 # Step-by-step install & troubleshooting
│   ├── active-response-rules/           # Custom Active Response rule definitions
│   └── agent-deployment-commands.md     # Linux/Windows agent enrollment commands
├── zabbix/
│   └── zabbix-setup-notes.md            # Zabbix 7.0 install & config steps
└── screenshots/
    ├── agents/                          # Agent list, deployment, agent manager
    ├── alerts/                          # Security alerts, auth failures, filtering
    ├── active-response/                 # Rule config + execution proof
    └── vulnerability-scan/              # Vulnerability assessment results
```

> Full VM images are **not included** (too large for GitHub) — only configs, install notes, and result screenshots are version-controlled.

---

## 📊 Results Summary

- ✅ Multiple agents (Linux + Windows) successfully enrolled and reporting to the Wazuh manager
- ✅ Centralized logging validated across all critical banking servers
- ✅ Real-time detection of failed logins / suspicious activity confirmed
- ✅ Active Response rule tested — automatic IP blocking on repeated auth failures
- ✅ Vulnerability scan completed with severity-classified findings
- ✅ Zabbix operational, tracking device/service health with automated alerting

---

## 🏦 About the Wider Project

The SOC work above was one component of a larger team project simulating a full three-tier banking network (Core/Distribution/Access) with FortiGate firewalls, VLAN segmentation, OSPF/HSRP redundancy, and a Linux-based server farm (DNS/DHCP/Mail/SFTP/Backup). Supervised by **Prof. Dr. Hamdy Hassan Elsayed**. This repo intentionally scopes down to the SOC portion I personally implemented.

---

## 📄 License

Shared for educational and portfolio purposes.
