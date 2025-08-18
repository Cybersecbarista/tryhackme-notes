# Networking Concepts

## OSI Model

The OSI (Open Systems Interconnection) model is a conceptual model developed by the ISO that describes how communications should occur in a computer network.

### The 7 Layers:
1. **Physical Layer** – Physical connection between devices (wires, optical, wireless).
2. **Data Link Layer** – Protocols enabling data transfer between nodes on the same segment (Ethernet, WiFi, MAC addresses).
3. **Network Layer** – Logical addressing and routing (IP, ICMP, VPN).
4. **Transport Layer** – End-to-end communication (TCP, UDP).
5. **Session Layer** – Establishing, maintaining, and synchronizing sessions (NFS, RPC).
6. **Presentation Layer** – Data encoding, compression, encryption (Unicode, MIME, JPEG).
7. **Application Layer** – Network services to applications (HTTP, FTP, DNS).

**Mnemonic:** “Please Do Not Throw Spinach Pizza Away.”

### OSI Summary Table
| Layer | Name              | Main Function                               | Examples |
|-------|-------------------|---------------------------------------------|----------|
| 7     | Application       | Services & interfaces to applications       | HTTP, FTP, DNS |
| 6     | Presentation      | Encoding, encryption, compression           | Unicode, JPEG |
| 5     | Session           | Establish/maintain/synchronize sessions     | NFS, RPC |
| 4     | Transport         | End-to-end communication, segmentation      | TCP, UDP |
| 3     | Network           | Logical addressing, routing                 | IP, ICMP |
| 2     | Data Link         | Reliable transfer between adjacent nodes    | Ethernet, WiFi |
| 1     | Physical          | Physical transmission media                 | Electrical, Optical, Wireless |

---

## TCP/IP Model

**Four-Layer Model:**
- Application Layer – Combines OSI layers 5–7.
- Transport Layer – Layer 4.
- Internet Layer – Layer 3.
- Link Layer – Layer 2.

**Five-Layer Internet Stack:**
1. Application
2. Transport
3. Network
4. Link
5. Physical

**Mapping Table:**
| OSI Layer        | TCP/IP Layer | Examples |
|------------------|-------------|----------|
| Application, Presentation, Session | Application | HTTP, FTP, SMTP |
| Transport        | Transport   | TCP, UDP |
| Network          | Internet    | IP, ICMP |
| Data Link        | Link        | Ethernet, WiFi |
| Physical         | Physical    | Cables, Radio |

---

## IP Addresses & Subnets

- IPv4: 32-bit address, 4 octets, each 0–255.
- Network & Broadcast addresses: `.0` and `.255`.
- CIDR notation: `/24` means first 24 bits are fixed.
- Private IP ranges (RFC 1918):
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16

**Lookup Commands:**
- Windows: `ipconfig`
- Linux: `ifconfig` or `ip a`

---

## Routing

- Routers operate at Layer 3.
- Forward packets based on IP addresses.
- May take multiple hops to destination.

---

## UDP & TCP

**UDP:**
- Connectionless, no delivery guarantee.
- Faster, used for streaming, DNS.
- Ports: 1–65535 (0 reserved).

**TCP:**
- Connection-oriented, reliable.
- Uses sequence and acknowledgment numbers.
- Three-way handshake: SYN → SYN-ACK → ACK.

---

## Encapsulation

1. Application data
2. Transport layer adds TCP/UDP header → segment/datagram
3. Network layer adds IP header → packet
4. Data link layer adds frame header/trailer → frame

Reverse process on receiving end.

---

## Life of a Packet

1. User sends data via application (HTTP request).
2. Transport layer (TCP) handles connection.
3. Network layer adds IP info.
4. Link layer transmits to router.
5. Routers forward until destination.

---

## TELNET

- Protocol for remote terminal access.
- Client connects to remote system via TCP port.

# Networking Essentials

## DHCP - Dynamic Host Configuration Protocol

When connecting to a network, your device must configure:
- **IP address** with subnet mask
- **Router** (gateway)
- **DNS server**

### Why DHCP?
- Automates network configuration
- Prevents IP conflicts
- Ideal for mobile devices

**Ports:**
- Server: UDP 67
- Client: UDP 68

### DHCP Process (DORA):
1. **Discover** – Client broadcasts `DHCPDISCOVER`
2. **Offer** – Server sends `DHCPOFFER`
3. **Request** – Client sends `DHCPREQUEST`
4. **Acknowledge** – Server sends `DHCPACK`

**Example packet capture:**
```
0.0.0.0 → 255.255.255.255  DHCP Discover
192.168.66.1 → 192.168.66.133  DHCP Offer
0.0.0.0 → 255.255.255.255  DHCP Request
192.168.66.1 → 192.168.66.133  DHCP ACK
```

DHCP provides:
- IP address
- Gateway
- DNS server

---

## ARP - Address Resolution Protocol

Maps **IP addresses (Layer 3)** to **MAC addresses (Layer 2)**.

### Example:
Host `192.168.66.89` → wants MAC for `192.168.66.1`  
Sends ARP Request → `ff:ff:ff:ff:ff:ff` (broadcast)  
Receives ARP Reply → `192.168.66.1 is at 44:df:65:d8:fe:6c`

**Key points:**
- Encapsulated directly in Ethernet frame (not IP/UDP)
- Layer 2 protocol but supports Layer 3 operations

---

## ICMP - Internet Control Message Protocol

Used for **diagnostics** and **error reporting**.

### Common Tools:
- **ping**: ICMP Echo Request (Type 8) & Echo Reply (Type 0)
- **traceroute**: Uses TTL field & ICMP Time Exceeded (Type 11)

### ping example:
```
ping 192.168.11.1 -c 4
4 packets transmitted, 4 received, 0% packet loss
rtt min/avg/max/mdev = 3.805/10.596/23.366/7.956 ms
```

### traceroute example:
```
traceroute example.com
1  192.168.66.1
2  192.168.11.1
...
16  93.184.215.14
```

---

## Routing Protocols

- **OSPF**: Link-state protocol, finds shortest path
- **EIGRP**: Cisco proprietary, hybrid routing
- **BGP**: Internet backbone routing between ISPs
- **RIP**: Simple, hop-count-based

---

## NAT - Network Address Translation

**Purpose:** Allow multiple devices to share a single public IP.

**Process:**
- Maps private IP + port → public IP + port
- Router keeps a translation table

**Example Mapping:**
| Internal IP   | Internal Port | Public IP   | Public Port |
|---------------|--------------|-------------|-------------|
| 192.168.0.129 | 15401        | 212.3.4.5   | 19273       |

# Networking Core Protocol Notes

## DNS - Remembering Addresses
DNS maps domain names to IP addresses so we don’t have to memorize IPs.  
- Operates at **Application Layer (Layer 7)** of OSI model.  
- Uses **UDP port 53** by default, **TCP port 53** as fallback.

### Common DNS Record Types:
- **A Record**: Maps hostname to IPv4 (e.g., example.com → 172.17.2.172)
- **AAAA Record**: Maps hostname to IPv6 (quad-A)
- **CNAME Record**: Maps domain name to another domain name
- **MX Record**: Specifies mail server for a domain

Example lookup:
```bash
nslookup www.example.com
```
Example packet capture:
```bash
tshark -r dns-query.pcapng -Nn
```

---

## WHOIS
- Provides registration info about a domain (registrant name, contact, creation date, etc.).
- Available via online tools or command-line `whois`.
- Can use privacy services to hide personal info.

---

## HTTP(S) - Accessing the Web
- **HTTP** = Hypertext Transfer Protocol
- **HTTPS** = HTTP Secure (encrypted via TLS)
- Relies on **TCP**.
- Common ports: **80 (HTTP)**, **443 (HTTPS)**, sometimes 8080, 8443.

### Common Methods:
- `GET`: Retrieve data
- `POST`: Submit data
- `PUT`: Create/replace data
- `DELETE`: Remove resource

Example manual HTTP request with telnet:
```bash
telnet MACHINE_IP 80
GET / HTTP/1.1
Host: anything
```

---

## FTP - Transferring Files
- Designed for file transfer (faster than HTTP in some cases).
- Default control port: **TCP 21**.

### Common FTP Commands:
- `USER`: Username
- `PASS`: Password
- `RETR`: Download file
- `STOR`: Upload file

---

## SMTP - Sending Email
- **Simple Mail Transfer Protocol**
- Default port: **TCP 25**.

### Common Commands:
- `HELO`/`EHLO`: Initiate session
- `MAIL FROM`: Sender email
- `RCPT TO`: Recipient email
- `DATA`: Begin message body
- `.` (alone): End of message

---

## POP3 - Receiving Email
- **Post Office Protocol v3**
- Default port: **TCP 110**.
- Retrieves and (usually) deletes emails from server.

### Common Commands:
- `USER <username>`
- `PASS <password>`
- `STAT`: Number & size of messages
- `LIST`: List messages
- `RETR <msg#>`: Retrieve message
- `DELE <msg#>`: Delete message
- `QUIT`: End session

---

## IMAP - Synchronizing Email
- **Internet Message Access Protocol**
- Default port: **TCP 143**.
- Synchronizes mailbox across devices (keeps emails on server).

### Common Commands:
- `LOGIN <username> <password>`
- `SELECT <mailbox>`
- `FETCH <mail#> <data_item>`
- `MOVE <sequence_set> <mailbox>`
- `COPY <sequence_set> <data_item>`
- `LOGOUT`

---

## Default Ports Summary Table

| Protocol | Transport | Port |
|----------|-----------|------|
| TELNET   | TCP       | 23   |
| DNS      | UDP/TCP   | 53   |
| HTTP     | TCP       | 80   |
| HTTPS    | TCP       | 443  |
| FTP      | TCP       | 21   |
| SMTP     | TCP       | 25   |
| POP3     | TCP       | 110  |
| IMAP     | TCP       | 143  |

---
# Networking Secure Protocols

## TLS (Transport Layer Security)

- **Historical Background**  
  - In the early 1990s, Netscape developed SSL (Secure Sockets Layer).  
  - SSL 2.0 released in 1995; TLS 1.0 introduced by IETF in 1999.  
  - TLS 1.3 released in 2018 with major improvements.  
  - TLS evolved over decades to ensure **confidentiality** and **integrity** of data.

- **How TLS Works**  
  - Operates at the **Transport Layer** of the OSI model.  
  - Provides **encryption** and **data integrity** for communication between client and server.  
  - Essential for secure online banking, shopping, and email.  
  - Common protocols upgraded with TLS:  
    - HTTP → **HTTPS**  
    - DNS → **DoT (DNS over TLS)**  
    - MQTT → **MQTTS**  
    - SIP → **SIPS**  

- **Certificates**  
  - Servers request a TLS certificate via a **Certificate Signing Request (CSR)** from a **Certificate Authority (CA)**.  
  - Certificates validate authenticity and prevent impersonation.  
  - **Let’s Encrypt** provides free certificates.  
  - **Self-signed certificates** exist but are not trusted by default.

---

## HTTPS (HTTP over TLS)

- **HTTP Recap**  
  - Operates over TCP port **80** by default.  
  - Traffic is sent in cleartext, vulnerable to eavesdropping.  

- **How HTTPS Works**  
  - Uses TLS on top of HTTP for secure communication.  
  - Default port: **443**.  
  - Process after DNS resolution:  
    1. TCP 3-way handshake  
    2. TLS handshake  
    3. HTTP request/response exchange  

- **Secure vs Insecure Ports**  

| Protocol | Insecure Port | Secure Port |
|----------|---------------|-------------|
| HTTP     | 80            | 443         |
| SMTP     | 25            | 465 / 587   |
| POP3     | 110           | 995         |
| IMAP     | 143           | 993         |

---

## SSH (Secure Shell)

- **Background**  
  - TELNET (port **23**) was insecure (cleartext communication).  
  - SSH developed in 1995 by Tatu Ylönen.  
  - SSH-2 introduced in 1996; OpenSSH released in 1999 (widely used today).  

- **Features**  
  - Secure authentication (password, public key, 2FA).  
  - Encryption ensures confidentiality.  
  - Integrity protection against tampering.  
  - **Tunneling** (VPN-like secure routing).  
  - **X11 Forwarding** for GUI apps.  
  - Default port: **22**.  

- **Usage Example**  
  ```bash
  ssh username@hostname
  ```

---

## SFTP vs FTPS

- **SFTP (SSH File Transfer Protocol)**  
  - Runs over **SSH (port 22)**.  
  - Uses Unix-like commands (`get filename`, `put filename`).  
  - Integrated within SSH suite.  

- **FTPS (File Transfer Protocol Secure)**  
  - FTP + TLS.  
  - Uses port **990**.  
  - Requires proper TLS certificate setup.  
  - Harder to configure behind strict firewalls due to separate control/data channels.  

---

## VPN (Virtual Private Network)

- **Purpose**  
  - Provides **private and encrypted communication** over insecure networks.  
  - Routes Internet traffic through a **VPN tunnel**.  

- **Benefits**  
  - Hides user’s IP address; only VPN server’s IP is visible.  
  - Protects against ISP surveillance and censorship.  
  - Allows bypassing of geo-restrictions.  

- **Considerations**  
  - Some VPN servers may **leak IP addresses** (check with DNS leak tests).  
  - VPN may be **illegal in some countries** – always verify local laws.  

---

## Summary

- TLS secures communication by encrypting data and verifying authenticity with certificates.  
- HTTPS, SMTPS, POP3S, and IMAPS are secure versions of core protocols.  
- SSH replaced TELNET with strong encryption and secure tunneling.  
- SFTP (over SSH) and FTPS (over TLS) both secure file transfers.  
- VPNs provide private communication but may have legal restrictions.  

# Wireshark: The Basics

Wireshark is an open-source, cross-platform network packet analyser tool capable of sniffing and investigating live traffic and inspecting packet captures (PCAP). It is commonly used as one of the best packet analysis tools.

## Tool Overview

### Use Cases
- Detecting and troubleshooting network problems, such as network load failure points and congestion.
- Detecting security anomalies, such as rogue hosts, abnormal port usage, and suspicious traffic.
- Investigating and learning protocol details, such as response codes and payload data.

> **Note:** Wireshark is not an Intrusion Detection System (IDS). It only allows analysts to discover and investigate the packets in depth. It also doesn't modify packets; it reads them. Detecting any anomaly or network problem highly relies on the analyst's knowledge and investigation skills.

## GUI and Data

Wireshark GUI opens with a single all-in-one page, which helps users investigate the traffic in multiple ways. At first glance, five sections stand out:

- **Toolbar:** Contains multiple menus and shortcuts for packet sniffing and processing, including filtering, sorting, summarising, exporting and merging.
- **Display Filter Bar:** The main query and filtering section.
- **Recent Files:** List of recently investigated files. You can recall listed files with a double-click. 
- **Capture Filter and Interfaces:** Capture filters and available sniffing points (network interfaces). 
- **Status Bar:** Tool status, profile and numeric packet information.

## PCAP Files

Packet details are shown in three different panes:

- **Packet List Pane:** Summary of each packet (source/destination addresses, protocol, info). Click to select a packet for further investigation.  
- **Packet Details Pane:** Detailed protocol breakdown of the selected packet.  
- **Packet Bytes Pane:** Hex and ASCII representation of the selected packet.  

## Colouring Packets

Wireshark colours packets based on conditions and protocols to help spot anomalies quickly.  
- **Temporary rules:** Available only during a program session.  
- **Permanent rules:** Saved under profile preferences and persist across sessions.  

Menus:  
- *View → Coloring Rules* (create permanent rules)  
- *View → Conversation Filter* (temporary rules)  

## Traffic Sniffing

- **Blue button:** Start capture  
- **Red button:** Stop capture  
- **Green button:** Restart capture  

## Merge PCAP Files

Use *File → Merge* to combine multiple PCAPs. Save the merged file before analysis.

## View File Details

View file metadata via *Statistics → Capture File Properties*. Useful for multiple PCAPs.  

## Packet Dissection

Wireshark decodes packet details by protocol. Packets can have 5–7 OSI layers.  

- **Frame (Layer 1):** Physical layer details.  
- **MAC (Layer 2):** Source & destination MAC addresses.  
- **IP (Layer 3):** Source & destination IPv4 addresses.  
- **Protocol (Layer 4):** TCP/UDP + ports.  
- **Protocol Errors:** Reassembly or errors.  
- **Application Protocol (Layer 5):** Details (HTTP, FTP, SMB).  
- **Application Data:** Application-specific payloads.  

## Packet Navigation

- **Packet Numbers:** Unique identifiers for packets.  
- **Go to Packet:** Navigate to a specific packet number.  
- **Find Packet:** Search by filter, hex, string, or regex.  
- **Mark Packets:** Highlight packets for analysis (resets after closing).  
- **Packet Comments:** Add notes that persist inside PCAP.  

## Exporting

- **Export Packets:** Share specific packets of interest.  
- **Export Objects (Files):** Extract transferred files (HTTP, SMB, TFTP, etc.).  

## Time Display Format

Default: seconds since capture start. Change via *View → Time Display Format*.  

## Expert Info

Wireshark highlights anomalies:  
- **Chat (Blue):** Informational  
- **Note (Cyan):** Notable events  
- **Warn (Yellow):** Warnings  
- **Error (Red):** Problems  

Groups include checksum errors, malformed packets, deprecated protocol usage, etc.

## Packet Filtering

Two filter types:  
- **Capture Filters:** Apply during collection.  
- **Display Filters:** Apply during analysis.  

Golden rule: *If you can click on it, you can filter and copy it.*  

### Filter Types
- **Apply as Filter:** Right-click to filter by field.  
- **Conversation Filter:** Show only related conversation packets.  
- **Colourise Conversation:** Highlight packets without filtering.  
- **Prepare as Filter:** Add filter query without execution.  
- **Apply as Column:** Add values as a column in the packet list.  

## Follow Stream

Reconstruct streams to see application-level data (e.g., HTTP/TCP).  
- Client → **Red**  
- Server → **Blue**  

Once a stream filter is applied, clear it with the “X” button to view all packets again.
# Tcpdump: The Basics

## Overview
The main challenge when studying networking protocols is that we don’t get a chance to see the protocol “conversations” taking place. All the technical complexities are hidden behind user interfaces. Tcpdump helps by capturing and displaying these packets in real time.

Tcpdump and its libpcap library were written in C/C++ and released in the late 1980s for Unix-like systems. They are stable, fast, and foundational for many other tools. On Windows, the ported version is known as **WinPcap**.

---

## Basic Packet Capture

- **Specify the Network Interface**
  ```bash
  tcpdump -i INTERFACE
  ```
  Example: `tcpdump -i eth0`  
  Use `-i any` to capture on all interfaces.

- **Save Captures to a File**
  ```bash
  tcpdump -w file.pcap
  ```
  Useful for later analysis in Wireshark.

- **Read from a Capture File**
  ```bash
  tcpdump -r file.pcap
  ```

- **Limit Number of Packets**
  ```bash
  tcpdump -c 10
  ```

- **Disable Resolution**
  ```bash
  tcpdump -n     # Don’t resolve IPs
  tcpdump -nn    # Don’t resolve IPs or ports
  ```

- **Verbose Output**
  ```bash
  tcpdump -v
  tcpdump -vv
  tcpdump -vvv
  ```

---

## Filtering Expressions

- **By Host**
  ```bash
  tcpdump host example.com
  tcpdump src host 192.168.1.1
  tcpdump dst host 192.168.1.50
  ```

- **By Port**
  ```bash
  tcpdump port 53
  tcpdump src port 22
  tcpdump dst port 443
  ```

- **By Protocol**
  ```bash
  tcpdump icmp
  tcpdump tcp
  tcpdump udp
  ```

- **Logical Operators**
  - `and` → both conditions  
  - `or` → either condition  
  - `not` → exclude condition  

  Example:  
  ```bash
  tcpdump host 1.1.1.1 and tcp
  tcpdump udp or icmp
  tcpdump not tcp
  ```

---

## Advanced Filtering

- **By Packet Size**
  ```bash
  tcpdump less 100
  tcpdump greater 512
  ```

- **By TCP Flags**
  ```bash
  tcpdump "tcp[tcpflags] == tcp-syn"
  tcpdump "tcp[tcpflags] & tcp-ack != 0"
  tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0"
  ```

---

## Displaying Packets

- **Quick Output**
  ```bash
  tcpdump -q
  ```

- **Include MAC Addresses**
  ```bash
  tcpdump -e
  ```

- **Show ASCII**
  ```bash
  tcpdump -A
  ```

- **Show Hexadecimal**
  ```bash
  tcpdump -xx
  ```

- **Show Hex + ASCII**
  ```bash
  tcpdump -X
  ```

---

## Command Summary

| Command                          | Explanation                                      |
|----------------------------------|--------------------------------------------------|
| `tcpdump -i INTERFACE`           | Capture on a given interface                     |
| `tcpdump -w FILE`                | Write to capture file                            |
| `tcpdump -r FILE`                | Read from capture file                           |
| `tcpdump -c COUNT`               | Limit number of packets captured                 |
| `tcpdump -n`                     | Don’t resolve IPs                                |
| `tcpdump -nn`                    | Don’t resolve IPs or ports                       |
| `tcpdump -v, -vv, -vvv`          | Increase verbosity                               |
| `tcpdump host IP/HOSTNAME`       | Filter by host                                   |
| `tcpdump port PORT`              | Filter by port                                   |
| `tcpdump icmp`                   | Filter by protocol                               |
| `tcpdump -q`                     | Quick output                                     |
| `tcpdump -e`                     | Show MAC addresses                               |
| `tcpdump -A`                     | Show ASCII                                       |
| `tcpdump -xx`                    | Show Hex                                         |
| `tcpdump -X`                     | Show Hex + ASCII                                 |

---

## Pro Tips

- Use `sudo` when capturing live traffic.  
- Save captures with `-w` and analyze in Wireshark.  
- Combine multiple filters for precision.  
- Exit tcpdump with `CTRL + C`.  
