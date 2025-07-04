User Behavior Anomaly Detection (UBAD) System
Automated Threat Detection with Splunk UBA, ES, CrowdStrike & SOAR

https://img.shields.io/badge/Splunk-CrowdStrike-blue
https://img.shields.io/badge/License-MIT-green

A production-ready detection system combining Splunk UBA, Enterprise Security (ES), CrowdStrike Falcon, and SOAR to identify and respond to insider threats, compromised accounts, and anomalous behavior.

📌 Table of Contents
Key Features

Architecture

Prerequisites

Installation

Configuration

Playbooks

Contributing

License

✨ Key Features
Real-time detection of:

Impossible travel

Privilege escalation

Data exfiltration

Malicious command execution

Automated containment via:

CrowdStrike (host isolation, process termination)

Active Directory (account disablement)

Forensic readiness: Memory dumps, process audits

SOC Integration: Slack/MS Teams alerts, ServiceNow ticketing

📐 Architecture
Diagram
Code











⚙️ Prerequisites
Component	Requirement
Splunk Enterprise	License for ES + UBA
CrowdStrike Falcon	API credentials (hosts:write scope)
Splunk SOAR	On-prem/Cloud instance
Python	3.8+ (for custom playbooks)
🚀 Installation
1. Splunk UBA Setup
bash
# Install UBA on CentOS/RHEL
sudo ./splunk-uba-installer.sh --accept-license
2. Configure Data Sources
Forward logs to Splunk from:

plaintext
- Active Directory (WinEventLogs)
- CrowdStrike Falcon (EDR)
- VPN/Proxy (Palo Alto, Zscaler)
3. Deploy SOAR Playbooks
Clone this repo and import playbooks:

bash
git clone https://github.com/yourrepo/ubad-system.git
cd ubad-system/playbooks
phantom playbook install impossible_travel_response.json
🔧 Configuration
Splunk ES Correlation Rules
splunk
# Example: Impossible travel + brute-force
`uba_impossible_travel` 
| join user [ 
    search `wineventlog_security` EventCode=4625 
    | stats count by user 
    | where count > 5 
] 
| `es_notable`
CrowdStrike API (SOAR Asset)
python
# In Splunk SOAR, configure assets/falcon.json
{
  "base_url": "https://api.crowdstrike.com",
  "client_id": "YOUR_CLIENT_ID",
  "client_secret": "YOUR_SECRET"
}
🤖 Automated SOAR Playbooks
Playbook	Trigger	Actions
isolate_host.py	UBA impossible travel	CrowdStrike host isolation + memory dump
kill_malicious_process.py	Suspicious PowerShell execution	Terminate process + ban hash
disable_ad_account.py	High-risk UBA anomaly	Disable AD account + notify SOC
Example Execution:

python
python3 playbooks/isolate_host.py --hostname WORKSTATION-123
🛠️ Contributing
Fork the repository

Create a branch (git checkout -b feature/improvement)

Submit a PR with tests

📜 License
MIT License - See LICENSE.

📞 Support
For issues, open a GitHub Issue.

🔐 Secure. Automated. Scalable.
Detect threats faster with behavior-based analytics!
