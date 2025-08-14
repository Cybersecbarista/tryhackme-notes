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
