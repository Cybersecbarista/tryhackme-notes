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
