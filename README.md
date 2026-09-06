# Building an Automated SOC Home Lab: From Telemetry to Orchestrated Response

## 🎯 Project Objective
The primary objective of this project was to bridge the gap between theoretical cybersecurity concepts and practical hands-on experience. I designed and deployed a fully functional, automated Security Operations Center (SOC) home lab to observe the entire lifecycle of a security event. The architecture ensures that when a security event occurs on an endpoint, telemetry flows seamlessly to a central Security Information and Event Management (SIEM) system, triggers an automated playbook for threat intelligence enrichment, and dynamically generates actionable incident tickets in a case management system alongside real-time analyst notifications.

## 📊 System Architecture & Data Flow

### 1. Logical Architecture Diagram
The high-level mapping shows how the virtual endpoint connects securely to our cloud monitoring infrastructure:

<img width="1408" height="768" alt="Logical Architecture Diagram" src="https://github.com/user-attachments/assets/ceb5c1f1-fbee-4641-a8cc-5c021113941c" />

### 2. Functional Data Flow Diagram
This overview maps out the exact 7-step network sequence from localized telemetry collection up to incident creation and analyst notification:

<img width="925" height="762" alt="High Overview of the Functional Diagram" src="https://github.com/user-attachments/assets/61d18a4e-04b0-413c-bb1b-e7fd795f7e3a" />

## 🧠 Skills Learned
- **Cloud Architecture & Resource Allocation:** Provisioning virtual infrastructure, configuring security firewall groups, and tailoring RAM allocations for indexing systems.
- **Endpoint Telemetry Engineering:** Deploying Sysmon schemas, configuring local agent configuration files (`ossec.conf`), and routing Event Logs to external managers.
- **SIEM Rule Customization:** Writing customized XML-based detection signatures to spot adversarial discovery commands (e.g., `whoami`).
- **SOAR Playbook Design:** Constructing multi-node logic flows, extracting text values utilizing regular expressions (regex), and managing API authentications.
- **Threat Intelligence Integration:** Interfacing automated web workflows with global reputation databases for live payload enrichment.
- **Enterprise Incident Management:** Structuring automated JSON requests to generate formal security cases with assigned severity within a triage team.

## 🛠 Tools Used
- **Wazuh:** Server-side SIEM & XDR platform used for centralized security log collection, decoding, and rule-based alerting.
- **Shuffle SOAR:** Security Orchestration, Automation, and Response platform utilized to build automated logic playbooks and webhooks.
- **TheHive:** An open-source, localized incident management and case tracking workspace for security analysts.
- **Sysmon (System Monitor):** A Windows system service configured with a modular rule schema to capture advanced endpoint telemetry.
- **VirusTotal API:** Open-Source Intelligence (OSINT) reputation engine used to automatically check file hash integrity.
- **Vultr Cloud Infrastructure:** Cloud hosting platform used to provision standalone virtual private servers for security applications.
- **PowerShell:** Command-line environment leveraged for secure remote administration (SSH) and deployment scripting.

## 📋 Step-by-Step Implementation

### Step 1: Cloud Infrastructure Deployment
- Provisioned two distinct cloud server instances using Vultr Virtual Private Servers configured with shared CPU resources to manage hosting overhead efficiently.
- Formed `MySOC-Wazuh` as the central SIEM manager node and `MySOC-TheHive` as the dedicated database and case management workstation.
- Established encrypted administrative tunnels to both systems utilizing administrative PowerShell SSH connections to process remote command deployments.

### Step 2: Wazuh SIEM Installation & Agent Rollout
- Initialized the Wazuh SIEM manager stack via a centralized installation script and secured web platform credentials.
- Set up internal system firewalls to permit encrypted web browser interactions through local secure port mappings (Port 443).
- Generated a customized endpoint deployment script to install the background Wazuh Monitoring Agent onto a target virtual Windows 11 platform.

### Step 3: Localized Data Stores & TheHive Cluster Configuration
- Configured core environment prerequisites on the Linux workstation including Amazon Corretto Java 11 engines.
- Installed Apache Cassandra to maintain back-end database structures and mapped cluster names alongside specific localized node interface variables (`rpc_address`).
- Deployed Elasticsearch to serve as the indexing system for prompt incident query processing.
- Completed installation steps for TheHive case engine and set up primary user profiles along with unique alphanumeric cryptographic API keys.

### Step 4: Endpoint Security Engineering & Rule Implementation
- Deployed Microsoft Sysmon on the Windows 11 endpoint using Olaf Hartong's configuration to log low-level process behavior.
- Modified the local `ossec.conf` file to actively monitor the `Microsoft-Windows-Sysmon/Operational` channel and forward logs to the Wazuh manager.
- Created a custom detection signature in `local_rules.xml` on the Wazuh server to trigger an alert whenever the command `whoami` is run.

### Step 5: End-to-End SOAR Playbook Automation
- Developed an automated security orchestration workflow using Shuffle SOAR initiated by a custom Webhook URL.
- Bound the Wazuh rule alert channel to forward all matching event payloads to Shuffle immediately upon detection.
- Integrated a regular expression string-capture node to isolate the 64-character SHA256 process execution hashes from the raw alerts.
- Routed the isolated hash to the VirusTotal API engine to enrich the alert with live global threat intelligence data.

### Step 6: Case Management & Analyst Notification
- Structured a POST request body inside Shuffle using a baseline JSON schema to pass SIEM alert details and VirusTotal reputation reports directly into TheHive, dynamically generating high-priority incident tickets.

<img width="975" height="562" alt="Shuffle_Connect_VirusTotal_To_TheHive_1" src="https://github.com/user-attachments/assets/84c8e942-91b2-4375-90aa-bbf175264ff3" />

- Configured an SMTP mail server action block inside Shuffle to immediately email the on-duty triage analyst team when a new case is generated.


<img width="1147" height="550" alt="Shuffle_Send_An_Email_1" src="https://github.com/user-attachments/assets/bd4d8d91-e3f4-41c9-98ca-5b2f2a4a0d48" />



<a href="https://medium.com/@ak-abderahim/building-an-automated-soc-home-lab-from-telemetry-to-orchestrated-response-14cbad6316e7" target="_blank" rel="noopener noreferrer">Read the full walkthrough here</a>
