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
In the previous task, we discussed the built-in firewall available in the Windows OS. What if you are a Linux user? You still need control over your network traffic. Linux also offers the functionality of a built-in firewall. We have multiple firewall options available here. Let’s briefly review most of them and explore one of them in detail.

Netfilter
Netfilter is the framework inside the Linux OS with core firewall functionalities, including packet filtering, NAT, and connection tracking. This framework serves as the foundation for various firewall utilities available in Linux to control network traffic. Some common firewall utilities that utilize this framework are listed below:

iptables: This is the most widely used utility in many Linux distributions. It uses the Netfilter framework that provides various functionalities to control network traffic.
nftables: It is a successor to the “iptables” utility, with enhanced packet filtering and NAT capabilities. It is also based on the Netfilter framework.
firewalld: This utility also operates on the Netfilter framework and has predefined rule sets. It works differently from the others and comes with different pre-built network zone configurations.
ufw 
ufw (Uncomplicated Firewall), as the name says, eliminates the complications of making rules in a complex syntax in “iptables”(or its successor) by giving you an easier interface. It is more beginner-friendly. Basically, whatever rules you need in “iptables”, you can define them with some easy commands via ufw, which would then be configuring your desired rules in “iptables”. Let’s have a look at some basic ufw commands down below.

To check the status of the firewall, you could use the command below:

Check status
user@ubuntu:~$ sudo ufw status
Status: inactive
If it appears inactive, you can enable it using the following command:

Enable
firewall
user@ubuntu:~$ sudo ufw enable
Firewall is active and enabled on system startup
To turn off the firewall, type “disable” instead of “enable” in the above command.

Below is a rule created to allow all the outgoing connections from a Linux machine. The default in the command means that we are defining this policy as a default policy allowing all the outgoing traffic unless we define an outgoing traffic restriction on any specific application in a separate rule. You can also make a rule to allow/deny traffic coming into your machine by replacing outgoing with incoming in the following command:

Allow all outgoing traffic
user@ubuntu:~$ sudo ufw default allow outgoing
Default outgoing policy changed to 'allow'
(be sure to update your rules accordingly)
You can deny incoming traffic at any port in your system. Let's say that we want to block incoming SSH traffic. We can achieve this with the command ufw deny 22/tcp. As you can see, we first specified the action, deny in this case; furthermore, we specified the port and the transport protocol, which is TCP port 22, or simply 22/tcp.

Deny incoming
SSH
traffic
user@ubuntu:~$ sudo ufw deny 22/tcp
Rule added
Rule added (v6)
To list down all the active rules in a numbered order, you can use the following command:

List all rules
user@ubuntu:~$ sudo ufw status numbered
     To                         Action      From
     --                         ------      ----
[ 1] 22/tcp                     DENY IN     Anywhere                  
[ 2] 22/tcp (v6)                DENY IN     Anywhere (v6)   
To delete any rule, execute the following command with the rule number to delete:

Delete a rule
user@ubuntu:~$ sudo ufw delete 2
Deleting:
 deny 22/tcp
Proceed with operation (y|n)? y
Rule deleted (v6)
These different utilities can be used to manage Netfilter. Choosing the right utility for the Linux OS depends on multiple factors, such as familiarity with the OS and your requirements. 
# IDS Fundamentals

## Overview
An **Intrusion Detection System (IDS)** monitors network or host activity to detect suspicious or malicious behavior that bypasses other security measures such as firewalls. It alerts security administrators when unusual activity is detected but does not take direct action to stop the activity.

Think of a **firewall** as a gatekeeper controlling what enters or leaves a building, and the **IDS** as the surveillance camera system that detects suspicious behavior once someone is inside.

---

## IDS Deployment Modes

### 1. Host Intrusion Detection System (HIDS)
- Installed directly on individual hosts.
- Detects threats related to that specific system.
- Provides deep visibility into host activities.
- Resource intensive and difficult to manage across large networks.

### 2. Network Intrusion Detection System (NIDS)
- Monitors overall network traffic across multiple hosts.
- Detects malicious activity throughout the entire network.
- Provides centralized detection and visibility.

**Key Difference:**  
HIDS focuses on a single host, while NIDS provides a network-wide perspective.

---

## IDS Detection Modes

### 1. Signature-Based IDS
- Detects known attacks using pre-defined patterns (signatures).
- Fast and reliable for known threats.
- Cannot detect **zero-day attacks** (no existing signature).
- Example: Snort (uses rule files containing signatures).

### 2. Anomaly-Based IDS
- Learns normal system/network behavior (baseline) and flags deviations.
- Capable of detecting **zero-day attacks**.
- Can generate **false positives** due to legitimate but unusual behavior.
- Accuracy improves through manual tuning and baseline refinement.

### 3. Hybrid IDS
- Combines **signature-based** and **anomaly-based** detection.
- Uses the best of both worlds: quick known threat detection and new threat awareness.
- Reduces the limitations of either approach.

---

## Snort IDS
**Snort** is a widely used open-source IDS developed in 1998. It supports both **signature** and **anomaly-based** detection methods.

### Snort Key Files
Located in `/etc/snort/` directory:
```
classification.config  reference.config  snort.debian.conf
community-sid-msg.map  rules             threshold.conf
gen-msg.map            snort.conf        unicode.map
```

- **snort.conf**: Main configuration file.
- **rules folder**: Contains built-in and custom detection rule files.

### Snort Rule Example
```bash
alert icmp any any -> 127.0.0.1 any (msg:"Loopback Ping Detected"; sid:10003; rev:1;)
```

#### Rule Components
| Component | Description |
|------------|-------------|
| **Action** | What Snort does when the rule triggers (e.g., `alert`). |
| **Protocol** | Protocol to monitor (e.g., `ICMP`). |
| **Source IP / Port** | Origin of the traffic (e.g., `any`). |
| **Destination IP / Port** | Destination (e.g., `$HOME_NET`). |
| **msg** | Alert message displayed when triggered. |
| **sid** | Unique signature ID for the rule. |
| **rev** | Revision number of the rule. |

---

## Snort Modes

| Mode | Description | Use Case |
|------|--------------|----------|
| **Packet Sniffer Mode** | Reads and displays network packets without analysis. | Used for network monitoring/troubleshooting. |
| **Packet Logging Mode** | Logs network traffic and detections for later analysis (PCAP format). | Forensics and root cause analysis. |
| **NIDS Mode** | Actively monitors live network traffic using rules and signatures. | Real-time intrusion detection. |

**Primary IDS Functionality:** NIDS mode is the most relevant for real-time detection.

---

## Running Snort for Detection

### Start Snort
```bash
sudo snort -q -l /var/log/snort -i lo -A console -c /etc/snort/snort.conf
```

- `-i lo`: Interface to monitor (e.g., loopback).
- `-A console`: Output alerts to the console.
- `-c`: Specifies configuration file.

### Test Rule
Ping your loopback interface to trigger the rule:
```bash
ping 127.0.0.1
```
**Example Output:**
```
07/24-10:46:52.401504  [**] [1:1000001:1] Loopback Ping Detected [**] [Priority: 0] {ICMP} 127.0.0.1 -> 127.0.0.1
```

---

## Running Snort on PCAP Files
Use Snort for forensic analysis on historical traffic logs:
```bash
sudo snort -q -l /var/log/snort -r Task.pcap -A console -c /etc/snort/snort.conf
```
Replace `Task.pcap` with your desired packet capture file.

---

## Key Takeaways
- **IDS = Network surveillance camera**: Detects, but doesn’t block.
- **HIDS vs NIDS**: Host-level vs Network-level focus.
- **Signature-based**: Known threats only.  
  **Anomaly-based**: Detects new/unknown threats.  
  **Hybrid**: Combines both.
- **Snort** is a powerful open-source IDS tool supporting real-time and offline analysis.
- Use **NIDS mode** for real-time alerts and **packet logging mode** for investigations.

---

### ✅ Summary
| Concept | Summary |
|----------|----------|
| **IDS Role** | Detect intrusions and alert administrators. |
| **Detection Methods** | Signature, Anomaly, Hybrid. |
| **Deployment Types** | HIDS, NIDS. |
| **Snort Functionality** | Packet capture, alerting, logging. |
| **Custom Rules** | Define detection behavior manually. |

---
**Author:** David Olivares  
**Topic:** TryHackMe – IDS Fundamentals  
**Date:** October 2025
