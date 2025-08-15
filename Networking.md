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

