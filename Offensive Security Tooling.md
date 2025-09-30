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

# Gobuster: The Basics

**Gobuster** is an open-source offensive tool written in Golang. It enumerates web directories, DNS subdomains, vhosts, Amazon S3 buckets, and Google Cloud Storage by brute force using wordlists and handling incoming responses. Security professionals use Gobuster for penetration testing, bug bounty hunting, and security assessments. In the phases of ethical hacking, Gobuster fits between **reconnaissance** and **scanning**.

---

## Concepts

### Enumeration
Enumeration is the act of listing all available resources (whether accessible or not). Example: Gobuster enumerates web directories.

### Brute Force
Brute force means trying every possibility until a match is found (like trying keys on a lock). Gobuster uses wordlists for brute forcing paths, subdomains, vhosts, etc.

---

## Overview
Gobuster is included by default in distributions like Kali Linux. Start by viewing the help page:

```bash
gobuster --help
```

Example output (truncated):

```
Usage:
  gobuster [command]

Available Commands:
  completion  Generate the autocompletion script for the specified shell
  dir         Uses directory/file enumeration mode
  dns         Uses DNS subdomain enumeration mode
  fuzz        Uses fuzzing mode. Replaces the keyword FUZZ in the URL, Headers and the request body
  gcs         Uses gcs bucket enumeration mode
  help        Help about any command
  s3          Uses aws bucket enumeration mode
  tftp        Uses TFTP enumeration mode
  version     shows the current version
  vhost       Uses VHOST enumeration mode (you most probably want to use the IP address as the URL parameter)
...
Flags:
  -t, --threads int           Number of concurrent threads (default 10)
  -w, --wordlist string       Path to the wordlist. Set to - to use STDIN.
  -o, --output string         Output file to write results to (defaults to stdout)
  --delay duration            Time each thread waits between requests (e.g. 1500ms)
  --debug                     Enable debug output
  --no-color                  Disable color output
```

> Use `gobuster [command] --help` for more information about a specific command.

### Common flags (summary)
| Short Flag | Long Flag | Description |
|---:|---|---|
| `-t` | `--threads` | Number of threads (default: 10) |
| `-w` | `--wordlist` | Path to the wordlist |
| `--delay` | | Delay between requests to avoid detection |
| `--debug` | | Enable debug output |
| `-o` | `--output` | Write results to file |

---

## Modes Covered
This guide focuses on three Gobuster modes used most often in web assessments:

1. `dir` — directory / file enumeration  
2. `dns` — DNS subdomain brute forcing  
3. `vhost` — virtual host brute forcing

---

## `dir` mode (directory enumeration)

- Purpose: Enumerate website directories and files (useful for discovering hidden files, admin panels, backups, etc).
- Basic command format:

```bash
gobuster dir -u "http://www.example.thm/" -w /path/to/wordlist -t 64
```

Explanation:
- `gobuster dir` — use dir mode.
- `-u "http://www.example.thm/"` — target URL (protocol required).
- `-w /path/to/wordlist` — wordlist to use (each entry appended to the URL).
- `-t 64` — threads.

### Useful `dir` flags
| Flag | Long Flag | Description |
|---:|---|---|
| `-c` | `--cookies` | Send cookies (e.g., session ID) |
| `-x` | `--extensions` | Comma-separated extensions to test (e.g., `.php,.js`) |
| `-H` | `--headers` | Custom headers to include |
| `-k` | `--no-tls-validation` | Skip TLS cert validation (useful for self-signed certs) |
| `-n` | `--no-status` | Hide status codes in output |
| `-P` | `--password` | Password for authenticated requests |
| `-U` | `--username` | Username for authenticated requests |
| `-r` | `--follow-redirect` | Follow HTTP redirects |
| `-s` | `--status-codes` | Show only specific status codes (e.g., `200,301`) |
| `-b` | `--status-codes-blacklist` | Hide specific status codes (overrides `-s`) |

### Example
```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r
```

Notes:
- Gobuster does **not** enumerate recursively; if a discovered directory looks interesting, run another Gobuster scan with that directory as the base path.
- Use correct protocol and hostname (use hostname rather than raw IP when virtual hosts matter).

---

## `dns` mode (subdomain enumeration)

- Purpose: Brute force DNS subdomains to discover hostnames that may expose different services or unpatched apps.
- Basic command format:

```bash
gobuster dns -d example.thm -w /path/to/wordlist
```

Explanation:
- `-d example.thm` — domain to enumerate.
- `-w` — wordlist of candidate subdomains (e.g., `admin`, `shop`, `api`).

### Useful `dns` flags
| Flag | Long Flag | Description |
|---:|---|---|
| `-c` | `--show-cname` | Show CNAME records (cannot be used with `-i`) |
| `-i` | `--show-ips` | Show IP addresses that domains resolve to |
| `-r` | `--resolver` | Use a custom DNS resolver |
| `-d` | `--domain` | The domain to enumerate |

### Example
```bash
gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

Example output (truncated):

```
Found: www.example.thm
Found: shop.example.thm
Found: academy.example.thm
```

Notes:
- Subdomains may host different versions of an application or services — always check them individually.

---

## `vhost` mode (virtual hosts)

- Purpose: Brute force virtual hosts (different hostnames served by the same machine/IP), by modifying the `Host:` header sent to the web server.
- Basic command format:

```bash
gobuster vhost -u "http://<IP-or-host>" -w /path/to/wordlist
```

Explanation:
- `gobuster vhost` — use vhost mode.
- `-u "http://10.201.78.153"` — base URL to send requests to (often an IP).
- `-w` — wordlist with hostnames to try (e.g., `blog`, `shop`).
- `--domain example.thm` — append domain parts to the Host header (e.g., `blog.example.thm`).
- `--append-domain` — append the configured domain to each wordlist entry.
- `--exclude-length` — filter results by response body length (helpful to remove false positives).

### How vhost works
Gobuster changes the `Host:` header for each request. Example GET request sent:

```
GET / HTTP/1.1
Host: www.example.thm
User-Agent: gobuster/3.6
...
```

By changing the `Host:` header to `blog.example.thm`, `shop.example.thm`, etc., Gobuster can detect virtual hosts served from the same IP.

### Useful `vhost` flags
| Flag | Long Flag | Description |
|---:|---|---|
| `-u` | `--url` | Base URL (target IP or hostname) |
| `--append-domain` | | Append domain to each wordlist entry |
| `-m` | `--method` | HTTP method (GET, POST, etc.) |
| `--domain` | | Domain to append to entries |
| `--exclude-length` | | Exclude results with specific response body lengths |
| `-r` | `--follow-redirect` | Follow redirects |

### Example
```bash
gobuster vhost -u "http://10.201.78.153" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320
```

Notes:
- `--exclude-length` is useful to filter out repetitive false positives (many false positives have similar response sizes).
- `vhost` differs from `dns`: `vhost` sends requests with modified Host headers to a target URL/IP, while `dns` performs DNS lookups for FQDNs.

---

## Summary / Key Takeaways

- **Gobuster** enumerates directories (`dir`), DNS subdomains (`dns`) and virtual hosts (`vhost`) using wordlists.
- `dir` mode helps find hidden files/directories and returns HTTP status codes to indicate accessible resources.
- `dns` mode brute-forces DNS to find additional subdomains which may host vulnerable services.
- `vhost` mode modifies the `Host:` header to discover multiple virtual hosts hosted on the same IP.
- Use flags like `--threads`, `--wordlist`, `--delay`, and `--exclude-length` to tune performance and reduce false positives.
- Always ensure you have **permission** to test a target; unauthorized scanning is illegal and unethical.

---

## Further reading & wordlists
- `/usr/share/wordlists/` (common location on Kali / AttackBox)  
- SecLists: `Discovery/DNS` and `Discovery/Web-Content` subfolders (useful wordlists)  
- Gobuster GitHub: https://github.com/OJ/gobuster

---

*Created from notes for a TryHackMe room: “Gobuster: The Basics” — formatted for GitHub and exported as `Gobuster_Basics.md`.*

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
