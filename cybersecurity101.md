# Search Skills - TryHackMe Notes

## Introduction

We are surrounded by information. Do you prefer to surrender in the face of information overload and accept the first few results you get? Or do you like to acquire the necessary search skills to find and access what you are looking for? This room aims to help you with the latter.

---

## Learning Objectives

The goal of this room is to teach:

- Evaluate information sources  
- Use search engines efficiently  
- Explore specialized search engines  
- Read technical documentation  
- Make use of social media  
- Check news outlets  

---

## Evaluation of Search Results

On the Internet, everyone can publish their writings. It can be in the form of blog posts, articles, or social media posts. It can be even in more subtle ways, such as by editing a public wiki page. This ability makes it possible for anyone to voice their unfounded claims. Everyone can express their opinion about best cyber security practices, future programming trends, and how to best prepare for a DevSecOps interview.

It is our job, as readers, to evaluate the information. Here are a few things to consider:

- **Source**: Identify the author or organization. Are they reputable?
- **Evidence and reasoning**: Are claims backed by credible evidence?
- **Objectivity and bias**: Is the information presented impartially?
- **Corroboration and consistency**: Can you find agreement from multiple sources?

---

## Search Engines

Most people use search engines, but few use them efficiently. Consider the following search engines:

- Google  
- Bing  
- DuckDuckGo  

### Common Search Operators (Google)

- `"exact phrase"` – Finds exact matches  
- `site:` – Restricts results to a specific domain (e.g., `site:tryhackme.com`)  
- `-` – Excludes a term (e.g., `pyramids -tourism`)  
- `filetype:` – Finds specific file types (e.g., `filetype:ppt cyber security`)  

---

## Specialized Search Engines

### Shodan

Search engine for devices connected to the Internet (e.g. Apache 2.4.1 servers).

### Censys

Focuses on Internet hosts, websites, certificates. Useful for:

- Enumerating domains  
- Auditing ports/services  
- Discovering rogue assets  

### VirusTotal

Scans files/URLs with multiple antivirus engines. Also supports hash lookup.

### Have I Been Pwned (HIBP)

Checks if your email has appeared in data breaches.

---

## Vulnerabilities and Exploits

### CVE

The CVE program provides a standard ID for vulnerabilities (e.g., CVE-2024-29988). Managed by MITRE.  
See: [CVE Website](https://cve.mitre.org) and [NVD](https://nvd.nist.gov)

### Exploit Database

Hosts verified and unverified exploits for security testing (with permission only).  
GitHub is also a rich source of PoCs and tools.

---

## Technical Documentation

### Linux Manual Pages

Use `man <command>` for official command documentation.

### Microsoft Docs

Microsoft provides technical documentation for its platforms.

### Product Docs

Always refer to official docs (e.g., Snort, Apache, PHP, Node.js) for:

- Latest updates  
- Full feature descriptions  

---

## Social Media and News

Social media is useful for:

- Tracking cybersecurity trends  
- Monitoring employee oversharing risks  
- Discovering vulnerabilities in real-time  

Follow cyber-focused channels and news outlets to stay updated.


# 🧠 Active Directory Basics

## 🏢 Introduction to Active Directory
Microsoft's Active Directory is the backbone of the corporate world. It simplifies the management of devices and users within a corporate environment.

### 🌐 Windows Domains
A Windows domain is a group of users and computers under centralized administration. The Domain Controller (DC) is the server that runs Active Directory services.

### ✅ Benefits
- Centralized identity management
- Manageable security policies

## 🧪 Real-World Example
In schools or offices, user credentials are validated across machines by the domain controller, which applies policies and restrictions centrally.

## 🧩 Active Directory Domain Services (AD DS)
Acts as a catalog for all network "objects":
- Users
- Machines
- Security groups
- Printers, etc.

### 👤 Users
- Represent people or services
- Can be authenticated and granted permissions
- Services like IIS/MSSQL use service accounts

### 💻 Machines
- Join the domain as objects (security principals)
- Named like `DC01$`
- Passwords rotated and long

### 🛡️ Security Groups
- Assign permissions to users/machines
- Nested groups allowed
- Common Groups:
  - Domain Admins
  - Server Operators
  - Backup Operators
  - Account Operators
  - Domain Users, Computers, Controllers

## 🗂️ Active Directory Users and Computers (ADUC)
Tool used to manage users/groups/machines in OUs:
- OUs mimic business structure
- Each user can belong to only one OU
- Containers:
  - Builtin
  - Computers
  - Domain Controllers
  - Users
  - Managed Service Accounts

## 📌 OUs vs Security Groups
| Organizational Units (OUs) | Security Groups |
|----------------------------|------------------|
| Used for policy application | Used for permission management |
| Only one OU per user        | Users can be in multiple groups |

## 🧑‍💻 Managing Users in AD

### 🔁 Delegation
Delegation allows giving specific privileges to users (like Helpdesk) to manage OUs without being Domain Admins.

## 🖥️ Managing Computers in AD
Default location: "Computers" container  
Best practice: Separate by function:
- Workstations (daily use, no elevated access)
- Servers (host services)
- Domain Controllers (most sensitive)

## ⚙️ Group Policies
GPOs let you apply settings to users/computers in an OU.

### 🛠️ Creating GPOs
1. Use Group Policy Management Tool
2. Create GPO under "Group Policy Objects"
3. Link GPO to target OU

### 🧰 Settings and Security Filtering
- GPOs apply to linked OU and sub-OUs
- Can restrict with Security Filtering (e.g., apply only to a group)

### 🔁 Distribution via SYSVOL
GPOs are distributed via:
```
\<domain>\SYSVOL
```

### 🕐 GPO Sync
- Syncs every 90–120 minutes
- Force sync with:
```bash
gpupdate /force
```

## 🔐 Authentication Methods

### Kerberos (Default)
- Uses tickets (TGT, TGS)
- Key Distribution Center (KDC) runs on Domain Controller
- Secure and efficient

### NetNTLM (Legacy)
- Challenge-response method
- Still used for compatibility
- Password hash never transmitted

## 🌳 Trees, Forests, Trusts

### Trees
- Domains in the same namespace
- Example: `uk.thm.local`, `us.thm.local` under `thm.local`

### Forests
- Domains with different namespaces
- Example: `thm.local` and `mht.local`

### Trust Relationships
- Allow cross-domain access
- One-way or two-way
- Trust ≠ access; permissions still need to be granted

---

## Conclusion

As the information landscape evolves, staying plugged into the right channels and resources helps you stay sharp and ahead of the curve.

# Windows Command Line Notes

> Everyone prefers a graphical user interface (GUI) until they master a command-line interface (CLI). There are many reasons for that.

GUIs are usually intuitive—you can explore and figure them out quickly. CLIs often have a learning curve, but once mastered, they can be faster and more efficient.

Example: Checking your IP address  
- GUI: Multiple clicks through menus.  
- CLI: Type one command, no mouse needed.

## Advantages of CLI
- **Lower resource usage**: Runs on older hardware or limited memory systems. Saves resources in cloud computing.
- **Automation**: Easy to script tasks with batch files.
- **Remote management**: Use SSH for servers, routers, IoT devices, even on slow networks.

---

## Basic System Information

**Commands:**

```cmd
set
```
Displays environment variables including the system `Path`.

```cmd
ver
```
Shows the Windows OS version.

```cmd
systeminfo
```
Displays detailed system information (OS, processor, memory, etc.).  
Use `| more` to view page-by-page.

```cmd
driverquery
driverquery | more
```
Lists drivers (page-by-page with `| more`).

```cmd
help
```
Help information for a command.

```cmd
cls
```
Clears the Command Prompt screen.

---

## Network Troubleshooting

**Network Configuration:**

```cmd
ipconfig
ipconfig /all
```
View basic or detailed network configuration.

**Connectivity Tests:**

```cmd
ping target_name
```
Check if a target is reachable.

```cmd
tracert target_name
```
Trace route to target.

**DNS Lookup:**

```cmd
nslookup example.com
nslookup example.com 1.1.1.1
```
Look up domain info (optional specific DNS server).

**Network Statistics:**

```cmd
netstat
netstat -abon
```
- `-a`: all connections/listening ports  
- `-b`: program using the port  
- `-o`: process ID  
- `-n`: numeric format

---

## File and Disk Management

**Directories:**

```cmd
cd
```
Show current directory.

```cmd
dir
dir /a
dir /s
```
List directory contents (`/a` for hidden, `/s` for subdirectories).

```cmd
tree
```
Graph view of directories.

```cmd
cd target_directory
cd ..
```
Navigate into or up directories.

```cmd
mkdir directory_name
rmdir directory_name
```
Create or remove directories.

**Files:**

```cmd
type file.txt
more file.txt
```
View text files (`more` for paging).

```cmd
copy source destination
move source destination
```
Copy or move files.

```cmd
del file.txt
erase file.txt
```
Delete files (`*` wildcard for multiple).

---

## Tasks and Process Management

```cmd
tasklist
```
List running processes.

```cmd
tasklist /FI "imagename eq sshd.exe"
```
Filter processes by name.

```cmd
taskkill /PID 4567
```
Kill process by PID.

---
# Windows PowerShell

## What is PowerShell?
From the official Microsoft page: “PowerShell is a cross-platform task automation solution made up of a command-line shell, a scripting language, and a configuration management framework.”

PowerShell is a powerful tool from Microsoft designed for task automation and configuration management. It combines a command-line interface and a scripting language built on the .NET framework. Unlike older text-based command-line tools, PowerShell is object-oriented, which means it can handle complex data types and interact with system components more effectively. Initially exclusive to Windows, PowerShell has lately expanded to support macOS and Linux, making it a versatile option for IT professionals across different operating systems.

## A Brief History of PowerShell
PowerShell was developed to overcome the limitations of existing command-line tools and scripting environments in Windows. In the early 2000s, as Windows was increasingly used in complex enterprise environments, traditional tools like cmd.exe and batch files fell short in automating and managing these systems. Microsoft needed a tool that could handle more sophisticated administrative tasks and interact with Windows’ modern APIs.

Jeffrey Snover, a Microsoft engineer, realised that Windows and Unix handled system operations differently—Windows used structured data and APIs, while Unix treated everything as text files. This difference made porting Unix tools to Windows impractical. Snover’s solution was to develop an object-oriented approach, combining scripting simplicity with the power of the .NET framework. Released in 2006, PowerShell allowed administrators to automate tasks more effectively by manipulating objects, offering deeper integration with Windows systems.

As IT environments evolved to include various operating systems, the need for a versatile automation tool grew. In 2016, Microsoft responded by releasing PowerShell Core, an open-source and cross-platform version that runs on Windows, macOS, and Linux.

## The Power in PowerShell
To fully grasp the power of PowerShell, we first need to understand what an object is in this context.

In programming, an object represents an item with properties (characteristics) and methods (actions). For example, a car object might have properties like `Color`, `Model`, and `FuelLevel`, and methods like `Drive()`, `HonkHorn()`, and `Refuel()`.

Similarly, in PowerShell, objects are fundamental units that encapsulate data and functionality, making it easier to manage and manipulate information. An object in PowerShell can contain file names, usernames or sizes as data (properties), and carry functions (methods) such as copying a file or stopping a process.

The traditional Command Shell’s basic commands are text-based, meaning they process and output data as plain text. Instead, when a cmdlet (pronounced command-let) is run in PowerShell, it returns objects that retain their properties and methods. This allows for more powerful and flexible data manipulation since these objects do not require additional parsing of text.

## PowerShell Basics

### Basic Syntax: Verb-Noun
PowerShell commands are known as **cmdlets**. They follow a `Verb-Noun` naming convention:

- **Verb**: Describes the action.
- **Noun**: Specifies the object of the action.

Examples:
- `Get-Content`: Retrieves the content of a file.
- `Set-Location`: Changes the current working directory.

### Basic Cmdlets
- `Get-Command`: Lists all available cmdlets, functions, aliases, and scripts.
- `Get-Help`: Provides detailed information about cmdlets, including usage and examples.
- `Get-Alias`: Lists all aliases (shortcuts) for cmdlets.

### Finding and Installing Cmdlets
- `Find-Module`: Searches online repositories like PowerShell Gallery.
- `Install-Module`: Installs a module from an online repository.

## Navigating the File System and Working with Files
- `Get-ChildItem`: Lists files and directories.
- `Set-Location`: Changes the current directory.
- `New-Item`: Creates a new file or directory.
- `Remove-Item`: Deletes a file or directory.
- `Copy-Item`: Copies a file or directory.
- `Move-Item`: Moves a file or directory.
- `Get-Content`: Displays the contents of a file.

## Piping, Filtering, and Sorting Data
- Piping (`|`) passes **objects** from one cmdlet to another.
- `Sort-Object`: Sorts objects by a property.
- `Where-Object`: Filters objects based on conditions.
- Comparison operators:
  - `-eq`: Equal to
  - `-ne`: Not equal to
  - `-gt`: Greater than
  - `-ge`: Greater than or equal to
  - `-lt`: Less than
  - `-le`: Less than or equal to
- `Select-Object`: Selects specific object properties or limits output.
- `Select-String`: Searches for text patterns in files (supports regex).

## System and Network Information
- `Get-ComputerInfo`: Retrieves comprehensive system information.
- `Get-LocalUser`: Lists local user accounts.
- `Get-NetIPConfiguration`: Displays network interface details.
- `Get-NetIPAddress`: Shows configured IP addresses.

## Real-Time System Analysis
- `Get-Process`: Lists running processes.
- `Get-Service`: Displays service statuses.
- `Get-NetTCPConnection`: Shows active TCP connections.
- `Get-FileHash`: Generates file hashes.

## Scripting in PowerShell
- Scripts automate repetitive tasks and can be defensive or offensive in cybersecurity.
- Blue team use cases: Log analysis, detecting anomalies, automating scans.
- Red team use cases: Enumeration, remote command execution, obfuscation.
- `Invoke-Command`: Executes commands on remote systems.


