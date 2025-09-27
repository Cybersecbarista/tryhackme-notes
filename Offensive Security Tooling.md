# Offensive Security Tooling — THC Hydra

**Summary:** Hydra is a fast, modular network login brute‑force tool that supports many protocols (SSH, FTP, HTTP forms, SMB, RDP, SMTP, and more). Use only with explicit permission during authorized assessments.

---

## Table of Contents
1. [Introduction](#introduction)
2. [Supported Protocols](#supported-protocols)
3. [Why strong passwords matter](#why-strong-passwords-matter)
4. [Basic Usage & Syntax](#basic-usage--syntax)
5. [Examples](#examples)
   - [FTP](#ftp)
   - [SSH](#ssh)
   - [HTTP POST (web form)](#http-post-web-form)
6. [Options & Cheat Sheet](#options--cheat-sheet)
7. [Notes & Best Practices](#notes--best-practices)
8. [References](#references)

---

## Introduction
Hydra is a brute force online password cracking program — a fast tool for automating login attempts across many services. It can iterate through username/password lists to discover valid credentials when weak or default credentials are in use.

Hydra is intended for authorized penetration testing and red‑team assessments. Always obtain written permission before testing any system you do not own.

## Supported Protocols
According to the official repository, Hydra supports a wide range of protocols, including (but not limited to):

> Asterisk, AFP, Cisco AAA, Cisco auth, Cisco enable, CVS, Firebird, FTP, HTTP-FORM-GET, HTTP-FORM-POST, HTTP-GET, HTTP-HEAD, HTTP-POST, HTTP-PROXY, HTTPS-FORM-GET, HTTPS-FORM-POST, HTTPS-GET, HTTPS-HEAD, HTTPS-POST, ICQ, IMAP, IRC, LDAP, MEMCACHED, MONGODB, MS-SQL, MYSQL, NCP, NNTP, Oracle Listener, Oracle SID, Oracle, PC-Anywhere, PCNFS, POP3, POSTGRES, Radmin, RDP, Rexec, Rlogin, Rsh, RTSP, SAP/R3, SIP, SMB, SMTP, SMTP Enum, SNMP v1+v2+v3, SOCKS5, SSH (v1 and v2), SSHKEY, Subversion, TeamSpeak (TS2), Telnet, VMware-Auth, VNC and XMPP.

For protocol‑specific options, consult Hydra's documentation or the Kali tools page for Hydra.

## Why strong passwords matter
Hydra demonstrates the danger of weak and default credentials. Common devices and services (CCTV, routers, web frameworks) sometimes ship with credentials like `admin:password`. Large wordlists (e.g., millions of entries) contain very common passwords — if you use weak passwords (short, no special characters, dictionary words), they will likely be discovered quickly.

## Basic Usage & Syntax
Hydra's basic invocation pattern requires a target, a service, and credentials (single or list):

```bash
hydra -l <username> -p <password> <target> <service>
```

Key flags used in examples below:

- `-l` : single username
- `-L` : username list (file)
- `-p` : single password
- `-P` : password list (file)
- `-t` : number of parallel threads
- `-V` : verbose (show each attempt)
- `-s` : service port (if non‑standard)
- `-e` : additional checks (`s` = try blank password, `n` = try "no pass", `r` = try reverse login/pass)
- `-f` : exit when a valid pair is found

## Examples

### FTP
Brute forcing FTP with a single username and a password list:
```bash
hydra -l user -P passlist.txt ftp://10.201.102.125
```

### SSH
Example (from your lab notes) — SSH brute force (4 threads):
```bash
hydra -l <username> -P /full/path/to/passlist.txt 10.201.102.125 -t 4 ssh
```

Explanation:
- `-l` specifies the SSH username
- `-P` indicates the path to a password list
- `-t 4` sets four parallel threads
- `ssh` is the service module to use

Concrete example:
```bash
hydra -l root -P passwords.txt 10.201.102.125 -t 4 ssh
```

### HTTP POST (Web Form)
Hydra can brute force form logins when you know the form parameters and the failure response string. Use the `http-post-form` module and provide the path, parameter format, and an indicator of failure.

Template:
```bash
hydra -l <username> -P <wordlist> <target> http-post-form "<path>:<login_fields>:<failure_string>" -V
```

Concrete example (from your notes):
```bash
hydra -l <username> -P <wordlist> 10.201.102.125 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V
```

Notes on the format:
- `/<path>` — the login page path (e.g., `/login.php` or `/` for root)
- `username=^USER^&password=^PASS^` — `^USER^` and `^PASS^` are placeholders Hydra replaces during attempts
- `F=incorrect` — Hydra will treat responses containing `"incorrect"` as a failed login indicator

If unsure whether a form is GET or POST, inspect the browser Developer Tools → Network tab while performing a login to see the exact request and parameters, or use Burp Suite to intercept and inspect the request.

## Options & Cheat Sheet
Quick reference flags and common combinations:

- `-l <user>` : single username  
- `-L <file>` : username list file  
- `-p <pass>` : single password  
- `-P <file>` : password list file  
- `-t <n>` : threads (parallel attempts)  
- `-V` : verbose output (show each attempt)  
- `-s <port>` : specify port if non‑standard (e.g., `-s 2222`)  
- `-e nsr` : extra checks (`n` blank, `s` try original password as username, `r` risky reverse)  
- `-f` : exit on first found credential pair

Example combinations:
```bash
hydra -L users.txt -P rockyou.txt 192.168.1.100 ssh -t 8 -V -f
hydra -l admin -P passwords.txt ftp://10.10.10.20 -t 6
hydra -l bob -P wordlist.txt 10.0.0.5 http-get /admin -V
```

## Notes & Best Practices
- **Authorization:** Always have explicit authorization before testing. Unauthorized brute forcing is illegal and unethical.
- **Wordlists:** Use targeted wordlists first (e.g., default passwords for the device, organization-themed words) before large lists to save time and avoid noisy traffic.
- **Account lockouts:** Be mindful of lockout or rate‑limiting mechanisms; brute forcing can lock accounts or trigger defenses.
- **Stealth & noise:** Hydra is noisy — consider slower thread counts, timing, and combining with proxy/intercept tools (Burp Suite) for web-based flows.
- **Logging:** Capture traffic (where allowed) with tcpdump/Wireshark or Burp for analysis and forensic evidence during engagements.
- **Combine tools:** Use Hydra alongside other reconnaissance tools to discover valid usernames, e.g., enum services, SMB enumeration, or web content discovery.

## References
- THC Hydra repository — https://github.com/vanhauser-thc/thc-hydra
- Kali tools — Hydra page — https://tools.kali.org/password-attacks/hydra
