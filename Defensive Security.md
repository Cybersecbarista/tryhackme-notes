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

---
