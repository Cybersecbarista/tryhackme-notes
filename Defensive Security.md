# SOC Fundamentals

Technology has made our lives more efficient, but with this efficiency comes more responsibility. Modern-day fears have come a long way from the exploitation of physical assets. The critical data, called secrets, are no longer stored in physical files. Organizations carry tons of confidential data in their network and systems. Any unauthorized disruption, loss, or modification to this data may cause huge damage. Threat actors discover and exploit new vulnerabilities in these networks and systems daily, becoming a major concern in cyber security. Traditional security practices may not be enough to prevent many of these threats. Dedicating a whole team to managing your organization’s security is important.

A **SOC (Security Operations Center)** is a dedicated facility operated by a specialized security team. This team continuously monitors an organization’s network and resources, identifying suspicious activity to prevent damage. The SOC operates **24/7/365**.

The main focus of the SOC team is **Detection and Response**. Security solutions integrate the company’s network and systems into one centralized location for continuous monitoring.

---

## Detection

- **Detect vulnerabilities**  
  A vulnerability is a weakness an attacker can exploit. For example, unpatched MS Windows computers. While fixing vulnerabilities is not strictly the SOC’s responsibility, unfixed vulnerabilities impact overall security.

- **Detect unauthorized activity**  
  Example: An attacker uses a stolen username/password to log in. SOC can identify unusual logins using clues like geographic location.

- **Detect policy violations**  
  Security policy violations differ by company. Examples:  
  - Downloading pirated media  
  - Sending confidential files insecurely  

- **Detect intrusions**  
  Intrusions = unauthorized access to systems/networks.  
  Example: Exploiting a vulnerable web application or visiting a malicious site.

---

## Response

- **Support with incident response**  
  Once an incident is detected, the SOC helps:  
  - Minimize impact  
  - Perform root cause analysis  
  - Support containment, eradication, and recovery

---

## The 3 Pillars of a SOC

1. **People**  
   Human expertise is vital. Security tools generate many alerts (false positives). Analysts filter, validate, and respond.  

2. **Process**  
   Clear workflows for triage, escalation, investigation, and response.  

3. **Technology**  
   Security solutions centralize logs, detect anomalies, and automate responses.  

A mature SOC requires **all three pillars** to work together.

---

## SOC Team Roles

- **SOC Analyst (Level 1)**  
  - First responders to detections  
  - Perform alert triage  
  - Report through proper channels  

- **SOC Analyst (Level 2)**  
  - Deeper investigation  
  - Correlate data from multiple sources  

- **SOC Analyst (Level 3)**  
  - Experienced threat hunters  
  - Handle critical incidents (containment, eradication, recovery)  

- **Security Engineer**  
  - Deploy/configure SOC security solutions  

- **Detection Engineer**  
  - Build detection rules behind security tools  

- **SOC Manager**  
  - Manages SOC processes and team  
  - Reports to the **CISO** on security posture  

> Note: Roles may vary depending on the size/criticality of the organization.

---

## SOC Processes

### Alert Triage

- First step for any alert = **triage**  
- Focused on analyzing the alert to determine severity & priority  
- Based on the **5 Ws**

#### Example Alert  
*Malware detected on Host: GEORGE PC*

| 5 Ws | Answers |
|------|---------|
| **What?** | Malicious file detected on a host |
| **When?** | 13:20, June 5, 2024 |
| **Where?** | Directory of host: "GEORGE PC" |
| **Who?** | User: George |
| **Why?** | File downloaded from pirated software site |

---

### Reporting

- Escalate harmful alerts to higher-level analysts  
- Escalation = tickets assigned to relevant people  
- Reports should include:  
  - 5 Ws  
  - Thorough analysis  
  - Evidence/screenshots  

---

### Incident Response & Forensics

- High-severity alerts may trigger **incident response**  
- Response includes containment, eradication, recovery  
- Forensics = deeper analysis of artifacts to determine root cause  

---

## SOC Technology

Security solutions minimize manual effort by centralizing information and automating detection/response.

- **SIEM (Security Information and Event Management)**  
  - Collects logs from multiple sources  
  - Detection rules flag suspicious activity  
  - Modern SIEM: user behavior analytics, threat intel, ML support  
  - Provides **Detection**, not response  

- **EDR (Endpoint Detection and Response)**  
  - Real-time/historical visibility at endpoint level  
  - Automated responses available  
  - Strong detection + investigation capabilities  

- **Firewall**  
  - Acts as barrier between internal & external networks  
  - Monitors traffic in/out  
  - Detects & blocks suspicious traffic  

- **Other Tools**  
  - Antivirus  
  - EPP (Endpoint Protection Platform)  
  - IDS/IPS  
  - XDR (Extended Detection & Response)  
  - SOAR (Security Orchestration, Automation, and Response)  

The right technology depends on organizational **threat surface** and **resources**.

# Digital Forensics Fundamentals

## Introduction
Forensics is the application of methods and procedures to investigate and solve crimes. The branch of forensics that investigates cyber crimes is known as **digital forensics**. Cyber crime is any criminal activity conducted on or using a digital device. Several tools and techniques are used to investigate digital devices thoroughly after any crime to find and analyze evidence for necessary legal action.

Digital devices have solved many of our problems, but due to their vast usage, an increase in **digital crimes (cyber crimes)** has also been observed.

---

## Case Example
Law enforcement raids a bank robber’s home and finds digital devices (laptop, mobile, hard drive, USB). The **digital forensics team** collects evidence and investigates, discovering:
- A digital map of the bank (planning evidence)
- Documents showing entrance/escape routes and physical security controls
- Media files (photos/videos of previous robberies)
- Chat groups and call records related to the robbery

This evidence supports **legal proceedings** and demonstrates the workflow from evidence collection to reporting.

---

## The Four Phases of Digital Forensics (NIST Framework)
The **National Institute of Standards and Technology (NIST)** defines a general digital forensics process with four main phases:

1. **Collection**
   - Identify and collect relevant digital devices (PCs, USBs, cameras, etc.).
   - Preserve integrity — ensure no tampering occurs.
   - Maintain detailed documentation of collected items.

2. **Examination**
   - Filter large data sets to isolate relevant data (e.g., files by date, user, or type).

3. **Analysis**
   - Correlate evidence to draw chronological conclusions about the incident.

4. **Reporting**
   - Document methodology, findings, and recommendations.
   - Include both technical details and executive summaries.

---

## Types of Digital Forensics
Each type uses unique collection and analysis methods:

- **Computer Forensics:** Investigating computers and storage media.
- **Mobile Forensics:** Extracting data such as texts, calls, GPS, and apps from mobile devices.
- **Network Forensics:** Investigating network traffic and logs.
- **Database Forensics:** Analyzing breaches or modifications within databases.
- **Cloud Forensics:** Investigating data stored in cloud environments.
- **Email Forensics:** Examining email communications for phishing or fraud evidence.

---

## Evidence Acquisition Best Practices

### 1. Proper Authorization
- Obtain legal approval before collecting any data.
- Unauthorized evidence may be inadmissible in court.

### 2. Chain of Custody
A **chain of custody document** ensures accountability and data integrity. It should include:
- Evidence description (name, type)
- Collector name
- Date/time of collection
- Storage location
- Access log (who accessed it and when)

### 3. Use of Write Blockers
Write blockers prevent modification of data during acquisition.  
Example: Attaching a suspect’s hard drive via a write blocker ensures timestamps and file integrity remain intact.

---

## Windows Forensics: Disk and Memory Imaging

Most cases involve **desktop/laptop systems** running Windows.  
Forensics images are **bit-by-bit copies** of the system:

### Disk Image
- Contains non-volatile data (files, history, documents).  
- Survives restarts.

### Memory Image
- Contains volatile data (open files, processes, network connections).  
- Must be captured **first**, as it disappears on shutdown.

### Popular Tools
| Tool | Purpose | Description |
|------|----------|-------------|
| **FTK Imager** | Disk Imaging | GUI-based; can create and analyze disk images. |
| **Autopsy** | Analysis | Open-source platform; supports keyword search, deleted file recovery, metadata extraction, etc. |
| **DumpIt** | Memory Imaging | CLI tool to capture RAM dumps. |
| **Volatility** | Memory Analysis | Open-source framework for analyzing volatile memory; supports multiple OS platforms. |

---

## Metadata and File Analysis

### Document Metadata (PDF Example)
Metadata stores information such as creator, creation date, and software used.

Example using `pdfinfo`:
```bash
pdfinfo DOCUMENT.pdf
```
Output example:
```
Creator:        Microsoft® Word for Office 365
Producer:       Microsoft® Word for Office 365
CreationDate:   Wed Oct 10 21:47:53 2018 EEST
Pages:          20
Encrypted:      no
PDF version:    1.7
```
This reveals details like creation date and originating software.

Install on Kali:
```bash
sudo apt install poppler-utils
```

---

### Image Metadata (EXIF Data)
**EXIF (Exchangeable Image File Format)** stores metadata in image files, including:
- Camera/phone model
- Capture date/time
- GPS coordinates (latitude & longitude)

Example using `exiftool`:
```bash
exiftool IMAGE.jpg
```
Output:
```
GPS Position : 51 deg 31' 4.00" N, 0 deg 5' 48.30" W
```

Coordinates can be entered into Google Maps or Bing Maps to locate where the image was taken.

Install on Kali:
```bash
sudo apt install libimage-exiftool-perl
```

---

## Summary
- **Digital Forensics** applies scientific processes to investigate cyber crimes.
- Follow NIST’s four-phase model: Collection → Examination → Analysis → Reporting.
- Preserve integrity using **authorization, chain of custody, and write blockers**.
- Use specialized tools (FTK Imager, Autopsy, DumpIt, Volatility) for disk/memory forensics.
- Analyze **metadata** for critical insights in documents and images.

---

**Author:** David Olivares  
**Platform:** [TryHackMe - Digital Forensics Fundamentals](https://tryhackme.com/)  
**Category:** Cybersecurity / Digital Forensics

---# 🛡️ Incident Response Fundamentals — TryHackMe Notes

**Author:** David Olivares  
**Platform:** TryHackMe  
**Topic:** Incident Response Fundamentals  
**Date:** 2025  

---

## 🧠 Introduction

Imagine living in a heavily insecure street with expensive items in your home. Naturally, you’d hire security guards, install CCTV cameras, and hide valuables underground — all proactive measures for protection.

Now, bring that concept into the **digital realm**. Organizations must also prepare against cyberattacks, plan preventive defenses, and have strategies ready **for when prevention fails**.  These preparations form the foundation of **Incident Response (IR)** — the systematic process of handling cybersecurity incidents from start to finish.

---

## ⚙️ Events, Alerts, and Incidents

Every computing device runs multiple **processes**, both interactive and non‑interactive, that generate **events** (logged records of actions). Security solutions collect and analyze these events to detect suspicious patterns.

When something abnormal is detected, a **security alert** is triggered.

### 🔍 Alert Types

| Type | Description | Example |
|------|--------------|----------|
| **False Positive** | Alert triggered for a benign activity | A data backup to cloud storage triggers a data‑exfiltration alert |
| **True Positive** | Alert that correctly identifies malicious behavior | A phishing email detected and confirmed as a real attack |

A **True Positive** becomes a **Security Incident** once verified by the security team.

### 🚨 Incident Severity Levels
Incidents are prioritized based on their impact:
- **Critical** – Requires immediate action; business‑stopping impact
- **High** – Major damage risk but not total outage
- **Medium** – Localized or contained damage
- **Low** – Minimal risk or easily mitigated

---

## 💥 Types of Security Incidents

| Type | Description |
|------|--------------|
| **Malware Infections** | Malicious software infecting systems via files or executables |
| **Security Breaches** | Unauthorized access to confidential data |
| **Data Leaks** | Exposure of sensitive data (accidental or intentional) |
| **Insider Attacks** | Attacks initiated by trusted personnel within an organization |
| **Denial of Service (DoS)** | Flooding systems or networks to make services unavailable |

🔸 Each type carries different impacts depending on the organization’s infrastructure and data value.

---

## 🧩 Incident Response Frameworks

Because incidents vary in nature and complexity, a **structured response process** is essential. Two major frameworks provide this structure:

- **SANS Incident Response (PICERL)**
- **NIST Incident Response Lifecycle**

Both outline logical steps to ensure incidents are handled efficiently and lessons are learned.

---

### 🧭 SANS Incident Response (PICERL)

| Phase | Description | Example |
|--------|--------------|----------|
| **P – Preparation** | Build teams, tools, and procedures before incidents occur | Employee phishing‑awareness training |
| **I – Identification** | Detect and confirm abnormal activities | Large outbound data transfer discovered and verified as compromise |
| **C – Containment** | Limit the spread and impact of the incident | Isolate infected host, disable compromised accounts |
| **E – Eradication** | Remove root cause and clean environment | Perform deep malware scans to remove threats |
| **R – Recovery** | Restore systems, validate, and resume operations | Rebuild system, restore data from backups |
| **L – Lessons Learned** | Review, document, and improve for the future | Post‑incident review and security improvements |

#### PICERL Flow Diagram
```
Preparation → Identification → Containment → Eradication → Recovery → Lessons Learned
```

---

### 🧭 NIST Incident Response Lifecycle

NIST defines **four phases**, similar in spirit but more condensed:

| Phase | Description |
|--------|--------------|
| **Preparation** | Establish policies, tools, and response capabilities |
| **Detection & Analysis** | Identify incidents using security solutions and logs |
| **Containment, Eradication & Recovery** | Respond, eliminate, and restore |
| **Post‑Incident Activity** | Review and improve the overall process |

#### NIST Flow Diagram
```
Preparation → Detection & Analysis → Containment/Eradication/Recovery → Post‑Incident Activity
```

---

### 🧮 Comparison: SANS vs NIST

| Aspect | SANS (6 Phases) | NIST (4 Phases) |
|---------|------------------|-----------------|
| Level of Detail | More granular | More streamlined |
| Emphasis | Focuses on full lifecycle and documentation | Focuses on detection and analysis |
| Use Case | Suited for large, mature SOC teams | Useful for standard corporate or government environments |

---

## 🧾 Incident Response Plan (IRP)

An **Incident Response Plan** is a formal document that defines how an organization prepares for, detects, and responds to incidents.

### 📋 Key Components
- **Roles & Responsibilities** — Defined tasks for IR team members
- **Response Methodology** — Steps to identify, contain, and recover
- **Communication Plan** — Coordination with stakeholders and law enforcement
- **Escalation Path** — Defined hierarchy for incident severity and response

---

## 🧰 Tools for Detection and Response

| Tool | Full Form | Function |
|------|------------|-----------|
| **SIEM** | Security Information and Event Management | Centralizes log collection and correlation for incident detection |
| **AV** | Antivirus | Detects and removes known malware |
| **EDR** | Endpoint Detection and Response | Detects, contains, and remediates advanced threats on endpoints |

These tools play critical roles across various stages of the IR lifecycle — from detection to containment.

---

## 📘 Playbooks & Runbooks

**Playbooks** are general step‑by‑step guides for specific types of incidents.

### Example: Phishing Email Playbook
1. Notify stakeholders of the phishing incident.
2. Analyze email headers and body for indicators of compromise (IoCs).
3. Examine any attachments and determine malicious intent.
4. Check whether attachments were opened.
5. Isolate infected systems from the network.
6. Block the malicious sender.

**Runbooks**, on the other hand, are more technical — outlining the precise commands or actions analysts should perform during investigation and containment.

---

## 🧩 Summary

In this TryHackMe room, we covered:
- The concept of **events → alerts → incidents**
- **True Positive** vs **False Positive** detection
- **Incident types** and how severity is classified
- The **SANS (PICERL)** and **NIST** frameworks for structured response
- The role of **SIEM, AV, and EDR tools** in detection and remediation
- The importance of **Incident Response Plans** and **Playbooks** for rapid, coordinated action

> 🧠 **Key Takeaway:** Incident Response isn’t just reaction — it’s preparation, process, and progression. Each incident is an opportunity to refine your defenses.

---

### ✍️ Authored by David Olivares
**TryHackMe Learning Journey | Cybersecurity Notes | © 2025**
# Logs Fundamentals

---

## 🔍 Overview
Attackers are clever. They often avoid leaving traces to prevent detection. However, through careful analysis of system **logs**, security teams can reconstruct what happened, determine how an attack was executed, and sometimes even identify who was responsible.

Logs act as **digital footprints**, recording activities that occur within a system — both legitimate and malicious. Investigating these logs allows analysts to trace actions and uncover the story behind an incident.

---

## 🧩 Real-World Analogy
Imagine investigating a robbery in a snowy cabin:
- **Broken door** → indicates forced entry
- **Footprints** → shows who entered and from where
- **CCTV footage** → provides evidence of the perpetrator

By piecing these clues together, the police identify the criminal. Similarly, in cybersecurity, **logs** are the digital equivalent of these clues.

---

## 🧠 Use Cases of Logs
| **Use Case** | **Description** |
|---------------|-----------------|
| **Security Events Monitoring** | Detect anomalous behavior using real-time monitoring. |
| **Incident Investigation & Forensics** | Perform root-cause analysis and identify what happened during incidents. |
| **Troubleshooting** | Diagnose errors in systems or applications using log records. |
| **Performance Monitoring** | Analyze logs for insights into system or application performance. |
| **Auditing & Compliance** | Maintain a verifiable record of activities for accountability and regulation. |

---

## 🧾 Log Categories
When investigating, it’s inefficient to look through every log file. Logs are categorized by type to make searching easier.

| **Log Type** | **Usage** | **Examples** |
|--------------|-----------|---------------|
| **System Logs** | Troubleshoot OS-level issues | System startup/shutdown, driver load, hardware events |
| **Security Logs** | Investigate security incidents | Authentication events, account changes, policy changes |
| **Application Logs** | Monitor app-specific events | User interactions, app updates, errors |
| **Audit Logs** | Track system and user changes | Data access, policy enforcement, system changes |
| **Network Logs** | Monitor network traffic | Incoming/outgoing traffic, firewall events |
| **Access Logs** | Record resource access | Web server access, API access, DB access |

> 💡 **Note:** Applications and services may create their own unique log types.

---

## 🪟 Windows Event Logs
Like other OSs, **Windows** maintains categorized logs accessible via the **Event Viewer** utility.

### Main Windows Log Types
- **Application Logs** → Record application-related events (errors, warnings, compatibility issues)
- **System Logs** → Record OS events (driver/hardware issues, startup/shutdown, services)
- **Security Logs** → Record security events (authentication, account changes, policy modifications)

### Opening Event Viewer
1. Click **Start → Search 'Event Viewer'**
2. Navigate to **Windows Logs** to view the main log categories.

### Event Fields
| **Field** | **Description** |
|------------|------------------|
| **Description** | Detailed information of the event |
| **Log Name** | Name of the log file |
| **Logged** | Timestamp of the event |
| **Event ID** | Unique identifier for a specific activity |

### Common Windows Event IDs
| **Event ID** | **Description** |
|---------------|------------------|
| 4624 | User account successfully logged in |
| 4625 | Failed login attempt |
| 4634 | User account logged off |
| 4720 | New user account created |
| 4724 | Password reset attempt |
| 4722 | User account enabled |
| 4725 | User account disabled |
| 4726 | User account deleted |

> 🎯 Tip: Use the **Filter Current Log** feature to search by specific Event IDs (e.g., `4624` for successful logins).

---

## 🌐 Web Server Access Logs (Apache Example)
Web servers log every request made to them. These logs are typically stored in:
```
/var/log/apache2/access.log
```
### Sample Fields
| **Field** | **Description** | **Example** |
|------------|-----------------|--------------|
| **IP Address** | Source of the request | 172.16.0.1 |
| **Timestamp** | Time of request | [06/Jun/2024:13:58:44] |
| **HTTP Method** | Requested action | GET |
| **URL** | Requested resource | /products |
| **Status Code** | Server response | 200, 404, 500 |
| **User-Agent** | Browser and OS details | Mozilla/5.0 (Windows NT 10.0...) |

---

## 💻 Manual Log Analysis in Linux
Log analysis can be done manually using common Linux command-line tools.

### 1. `cat` — View File Contents
Display contents of a log file:
```bash
cat access.log
```
Combine multiple log files:
```bash
cat access1.log access2.log > combined_access.log
```

### 2. `grep` — Search for Patterns
Search for a specific IP or keyword inside logs:
```bash
grep "192.168.1.1" access.log
```

### 3. `less` — Paginated Log Viewing
View logs page-by-page for easier navigation:
```bash
less access.log
```

- Press **Spacebar** → Next page
- Press **b** → Previous page
- Press **/** followed by a term → Search
- Press **n / N** → Move between results

---

## 🧠 Summary
- Logs are the **digital footprints** of all system and user activities.
- Categorizing logs improves **investigation efficiency**.
- **Windows Event Viewer** simplifies viewing and filtering.
- **Command-line utilities** like `cat`, `grep`, and `less` enable efficient log analysis.

> 🔒 **Key Takeaway:** Effective log analysis bridges the gap between raw data and actionable cybersecurity insight.
