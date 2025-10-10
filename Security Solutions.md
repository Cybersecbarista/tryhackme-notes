# 🛡️ Cyber Security Solutions — Introduction to SIEM

## What is SIEM?

**SIEM (Security Information and Event Management)** is a system that collects data from multiple endpoints and network devices, centralizes it, and performs correlation for security visibility and incident detection.

### Key Components
- **Host-Centric Log Sources**: Capture events within or related to a host.
  - Examples: Windows Event Logs, Sysmon, Osquery
  - Common events:
    - File access
    - User authentication attempts
    - Process execution
    - Registry changes
    - PowerShell activity

- **Network-Centric Log Sources**: Capture events during host communication or external access.
  - Examples: SSH, VPN, HTTP/S, FTP
  - Common events:
    - SSH connection
    - FTP file access
    - Web traffic
    - VPN usage
    - Network file sharing

---

## Importance of SIEM

As devices generate thousands of logs per second, manually reviewing them is inefficient. **SIEM centralizes, correlates, and analyzes** logs to detect anomalies and respond quickly.

### Core Features
- Real-time log ingestion
- Alerting on abnormal activity
- 24/7 monitoring and visibility
- Early threat detection
- Data visualization and insights
- Incident investigation capability

---

## Common Log Sources

### 🪟 Windows Machine
- Uses **Event Viewer** to track all activities via event IDs.
- Common log sources are forwarded to SIEM for centralized monitoring.

### 🐧 Linux Workstation
- Logs stored in `/var/log` directories:
  - `/var/log/httpd` → HTTP requests and errors
  - `/var/log/cron` → Cron job events
  - `/var/log/auth.log` or `/var/log/secure` → Authentication
  - `/var/log/kern` → Kernel-level logs

**Sample cron log:**
```bash
May 28 13:04:20 ebr crond[2843]: /usr/sbin/crond 4.4 started with loglevel notice
Jun 13 07:46:22 ebr crond[3592]: unable to exec /usr/sbin/sendmail
```

### 🌐 Web Server
- Apache logs help detect web attacks.
- Common paths: `/var/log/apache` or `/var/log/httpd`

**Example:**
```bash
192.168.21.200 - - [21/March/2022:10:17:10 -0300] "GET /cgi-bin/try/ HTTP/1.0" 200 3395
127.0.0.1 - - [21/March/2022:10:22:04 -0300] "GET / HTTP/1.0" 200 2216
```

---

## Log Ingestion Methods

1. **Agent / Forwarder** — Installed tool that captures logs and sends to SIEM (e.g., Splunk Forwarder).
2. **Syslog** — Widely used protocol for centralized logging.
3. **Manual Upload** — Allows importing offline data for analysis.
4. **Port Forwarding** — Endpoints send data to SIEM via configured ports.

---

## SIEM Capabilities

- Correlation between multiple log sources
- Host and network visibility
- Threat hunting and rule-based detection
- Timely incident response

### SIEM in SOC (Security Operations Center)
Acts as the **central nervous system** of SOC operations:
- Collects logs
- Detects anomalies
- Triggers alerts based on correlation rules

---

## SOC Analyst Responsibilities

- Continuous monitoring and investigation
- Identifying false positives
- Rule tuning and noise reduction
- Reporting and compliance
- Closing network visibility gaps

---

## Dashboards

Dashboards summarize and visualize data for actionable insights.

**Common Dashboard Elements:**
- Alert highlights
- System notifications
- Health status
- Failed login attempts
- Ingested event counts
- Triggered rules
- Top visited domains

Example: *QRadar Default Dashboard*

---

## Correlation Rules

Logical conditions that trigger alerts when matched.

### Examples:
- 5 failed logins in 10 seconds → Alert: *Multiple Failed Login Attempts*
- Successful login after multiple failed logins → Alert: *Suspicious Success*
- USB insertion → Alert: *Unauthorized Device*
- Outbound traffic > 25 MB → Alert: *Possible Data Exfiltration*

### Rule Creation Examples

**Use Case 1 — Log Deletion Detection:**
```text
IF LogSource = WinEventLog AND EventID = 104 → ALERT: Event Logs Cleared
```

**Use Case 2 — Privilege Escalation (whoami):**
```text
IF LogSource = WinEventLog AND EventID = 4688 AND NewProcessName CONTAINS "whoami"
→ ALERT: WHOAMI Command Execution Detected
```

---

## Alert Investigation

After a rule triggers, analysts investigate to determine if the alert is valid.

### Investigation Steps
1. Review event details and rule conditions.
2. Determine **True Positive** or **False Positive**.
3. If false, tune rule to prevent similar noise.
4. If true:
   - Contact asset owner
   - Isolate infected host
   - Block malicious IP

---

### 🧩 Summary

- SIEM provides **visibility, detection, and response** capabilities.
- It enables security teams to act on threats quickly.
- Dashboards and correlation rules form the backbone of effective monitoring.
- Analysts ensure continuous improvement via tuning and investigation.

> “SIEM is not just a tool—it’s the nerve center of modern cybersecurity defense.”
