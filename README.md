
---

## 🛡️ Project Report: Cloud Threat Detection using Microsoft Sentinel

---

### 📌 Project Title:  
**Cloud Threat Detection using Microsoft Sentinel and Azure Log Analytics**

---

### 🧩 Objective:
The purpose of this project is to design and implement a cloud-native cybersecurity monitoring solution using Microsoft Azure. The system uses **Microsoft Sentinel**, a SIEM/SOAR solution, to detect, analyze, and respond to threats in a cloud environment.

---

### 🔧 Tools & Technologies Used:
- **Microsoft Azure**
  - Azure Sentinel
  - Log Analytics Workspace
  - Azure Virtual Machines (Linux/Windows)
  - Microsoft Defender for Cloud
  - Azure Logic Apps (optional for automation)
- **Kusto Query Language (KQL)** for log analysis
- **Atomic Red Team** (optional, for simulating attacks)

---

### 🏗️ Architecture Overview:
```
+-------------------+         +------------------------+
| Azure VM          |         | Azure Resources        |
| (Log Source)      | ---->   | (Azure AD, Defender)   |
+-------------------+         +------------------------+
         |                            |
         v                            v
+-----------------------------------------------------+
|     Azure Log Analytics Workspace                   |
|     (Collects and stores logs & telemetry data)     |
+-----------------------------------------------------+
         |
         v
+-----------------------------------------------------+
| Microsoft Sentinel                                  |
| - Security Analytics Rules                          |
| - Incident Detection                                |
| - Workbooks & Dashboards                            |
| - Automation (Logic Apps)                           |
+-----------------------------------------------------+
```

---

### 🪜 Step-by-Step Implementation:

#### 1️⃣ Create Log Analytics Workspace
- Go to Azure Portal → Search "Log Analytics Workspace"
- Create a new workspace:  
  - Region: East US  
  - Pricing Tier: Pay-as-you-go (free tier is enough for small projects)

#### 2️⃣ Enable Microsoft Sentinel
- Go to Sentinel → “+ Add” → Select your workspace
- Microsoft Sentinel is now linked to the workspace

#### 3️⃣ Deploy a Virtual Machine
- Azure Portal → Create VM (Ubuntu or Windows)
- Enable **Monitoring** and **Boot diagnostics**
- Install Sysmon or enable Security Auditing (Windows) for rich logs

#### 4️⃣ Connect Data Sources
- In Sentinel → Data connectors
- Connect:
  - **Azure Activity Logs**
  - **Azure AD Logs**
  - **Security Center**
  - **VM logs** (via diagnostic settings)

#### 5️⃣ Configure Diagnostic Settings on VM
- Go to your VM → Monitoring → Diagnostic Settings
- Forward logs to your Log Analytics Workspace

#### 6️⃣ Create Analytics Rules
- In Sentinel → Analytics → + Create Rule
- Sample use cases:
  - Brute-force RDP attempts
  - Multiple failed login attempts
  - Execution of suspicious PowerShell commands

Example KQL Rule:
```kql
SecurityEvent 
| where EventID == 4625 
| summarize FailedAttempts = count() by Account, IPAddress, bin(TimeGenerated, 1h)
| where FailedAttempts > 5
```

#### 7️⃣ Create Workbooks
- Go to Sentinel → Workbooks → + New
- Visualize trends: failed logins, top IP addresses, etc.

#### 8️⃣ (Optional) Automate Response using Playbooks
- Create a Logic App that triggers:
  - Email notification
  - Disable user
  - Block IP

---

### 💻 Simulated Attack (Optional)
- Use **Atomic Red Team** or **manual brute-force attempts** to generate logs
- Observe alerts and responses in Sentinel

---

### 📊 Sample Outputs (include in your report):
- Screenshot of:
  - Log Analytics query results
  - Triggered Sentinel alerts
  - Dashboard/Workbook
  - Incident details
  - Logic App (if used)

---

### 📘 Learning Outcomes:
- Understanding of Azure SIEM (Sentinel)
- Experience with KQL for threat hunting
- Basic incident detection and automation
- Familiarity with Microsoft Defender and Azure Monitoring

---

### 📂 Project Repository Structure (Optional for GitHub):

```
azure-threat-detection/
│
├── 📄 README.md
├── 📁 KQL-Queries/
│   └── failed-logins.kql
├── 📁 Screenshots/
│   └── sentinel-alerts.png
├── 📁 Workbooks/
│   └── dashboard.json
├── 📁 LogicApps/
│   └── auto-email-alert.json
└── 📄 Report.pdf
```

---

### 📅 Timeline:
| Task                          | Duration       |
|-------------------------------|----------------|
| Setting up Azure resources    | 1 day          |
| Configuring Sentinel          | 1 day          |
| Simulating attacks            | 1–2 days       |
| Creating dashboards & rules   | 1 day          |
| Documentation                 | 1 day          |

---

### ✅ Conclusion:
This project provides a foundational understanding of building a **cloud-native threat detection** system using Microsoft Azure Sentinel. It demonstrates the ability to ingest logs, write detection queries, visualize attack patterns, and build automated responses — skills essential in cloud security roles.

---
