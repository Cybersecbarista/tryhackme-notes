# Network Fundamentals – TryHackMe Notes

## Section 1: What is Networking?
- Networks are any devices connected to each other.
- In computing, networking refers to technological devices being connected.
- The internet is a large network made of smaller private and public networks.
- The first iteration was ARPANET in the late 1960s.
- Tim Berners-Lee invented the World Wide Web.

## Section 2: Identifying Networks on a Device
- Devices use two key identifiers:
  - **IP Address**: Temporary, identifies a host on a network.
  - **MAC Address**: Permanent hardware ID.
- IP addresses are made of 4 octets (e.g., 192.168.1.1).
- Private vs Public IPs:
  - Public identifies a device on the internet.
  - Private identifies a device among local devices.
- **MAC Address**: 12-character hexadecimal, e.g., `a4:c3:f0:85:ac:2d`.
- Spoofing = pretending to be another MAC address.
- **Ping**: Uses ICMP to check network connectivity.
  - Syntax: `ping [IP or domain]`
  - Example: `ping 192.168.1.254`

# Introduction to LAN

## LAN Topologies
### Star Topology
- Devices connect via a central switch or hub.
- Reliable, scalable, but requires more hardware.
### Bus Topology
- Single backbone cable all devices connect to.
- Simple and cheap, but prone to bottlenecks and faults.
### Ring Topology
- Devices form a closed loop.
- Data travels in one direction using a token.
- Less hardware, but network breaks if a single device/cable fails.

## Network Devices

### What is a Switch?
- Aggregates devices using Ethernet.
- Sends packets only to the intended target.
- Found in large environments (offices, schools).

### What is a Router?
- Connects multiple networks.
- Uses routing to deliver data.
- Useful for pathfinding in complex networks.

## Subnetting
- Divides one network into smaller sub-networks.
- **Subnet mask** determines the range of devices.
- **Used to identify**:
  - Network Address
  - Host Address
  - Default Gateway

## ARP (Address Resolution Protocol)
- Maps IP addresses to MAC addresses.
- Each device has an ARP cache.
- Uses:
  - **ARP Request**: "Who has this IP?"
  - **ARP Reply**: Response with MAC address.

## DHCP (Dynamic Host Configuration Protocol)
- Automatically assigns IP addresses.
- Process:
  - **DHCP Discover** → **DHCP Offer** → **DHCP Request** → **DHCP ACK**
 
  - # OSI Model

## What is the OSI Model?

The **OSI Model (Open Systems Interconnection Model)** provides a framework dictating how all network devices will send, receive, and interpret data.

### Benefits:
- Devices can have different functions and designs while still communicating effectively.
- Ensures that data sent across a network can be universally understood.

### OSI Model Layers (Top to Bottom):
7. Application  
6. Presentation  
5. Session  
4. Transport  
3. Network  
2. Data Link  
1. Physical

### Encapsulation:
At every layer data travels through, specific processes take place, and new headers or instructions are added.

---

## Layers of the OSI Model

### 1. Physical Layer
- Deals with physical components of network hardware.
- Transfers data using electrical signals in binary (1s and 0s).
- **Example:** Ethernet cables.

### 2. Data Link Layer
- Focuses on physical (MAC) addressing.
- Adds MAC address to packets.
- Uses the NIC (Network Interface Card), which contains a unique MAC address.
- Formats data for physical transmission.

### 3. Network Layer
- Handles routing and reassembly of data packets.
- Determines best path using protocols like **OSPF** and **RIP**.
- Routing decisions depend on:
  - Shortest path
  - Reliability (packet loss history)
  - Physical connection speed (copper vs fiber)
- Uses **IP addresses** (e.g., `192.168.1.100`).
- **Routers** are Layer 3 devices.

### 4. Transport Layer
- Ensures proper transmission of data between devices.
- Uses **TCP** and **UDP**.

#### Transmission Control Protocol (TCP)
- Connection-oriented and reliable.
- Keeps a constant connection during transmission.
- Includes error checking and ordered delivery.
- **Pros:** Accuracy, flow control, error recovery.
- **Cons:** Slower, requires stable connection.

**Used for:** File transfers, web browsing, emails.

#### User Datagram Protocol (UDP)
- Connectionless and fast.
- No error checking or delivery guarantee.
- **Pros:** Speed, lightweight, minimal resource use.
- **Cons:** Unreliable on unstable connections.

**Used for:** ARP, DHCP, video streaming, device discovery.

### 5. Session Layer
- Manages and maintains connections (sessions).
- Creates and terminates sessions.
- Uses checkpoints to save bandwidth during reconnections.
- Each session is isolated.

### 6. Presentation Layer
- Acts as translator between systems.
- Converts and standardizes data formats.
- Handles encryption/decryption (e.g., HTTPS).

### 7. Application Layer
- Provides interface for user interaction with data.
- Uses GUI-based applications.
- Example protocols: **DNS** (translates domain names to IPs).

---
## 📦 Packets and Frames

### 🔍 What Are Packets and Frames?
- Small pieces of data that, when combined, form a larger piece of information or message.
- Packets and frames operate at different layers in the OSI model:
  - **Frame**: Layer 2 (Data Link Layer) — contains no IP address information.
  - **Packet**: Layer 3 (Network Layer) — includes IP address info.
- **Encapsulation**: Like putting an envelope (packet) inside another envelope (frame).
- Once the encapsulating data is removed, the **frame** is exposed.
- Packets improve efficiency by breaking large messages into smaller, manageable pieces.

### 📜 Packet Structure and Headers
- Networking follows standards and protocols that define how packets are created, sent, and received.
- **Packet headers** (common with Internet Protocol):
  - **Time To Live (TTL)**: Sets an expiry time to prevent network clogging.
  - **Checksum**: Ensures data integrity (used in TCP/IP).
  - **Source Address**: IP address of the sending device.
  - **Destination Address**: IP address of the receiving device.

---

## 🔁 TCP/IP and the Three-Way Handshake

### 🌐 TCP (Transmission Control Protocol)
- A connection-based protocol that ensures data delivery via a **three-way handshake**.
- TCP is structured into 4 layers:
  1. Application  
  2. Transport  
  3. Internet  
  4. Network Interface  
- TCP adds headers at each layer (encapsulation). Removing them is **decapsulation**.

### ✅ Advantages of TCP
- Guarantees data integrity.
- Prevents packet flooding by synchronizing transmission.
- Reliable, ordered, and error-checked delivery.

### ⚠️ Disadvantages of TCP
- Requires stable connection between devices.
- Slower than UDP due to overhead.
- If part of a message is lost, it must be resent.

---

### 📦 TCP Packet Headers
- **Source Port**: Random port opened by sender (0–65535).
- **Destination Port**: Port of receiving service (e.g., 80 for HTTP).
- **Source IP / Destination IP**: IP addresses of sender and receiver.
- **Sequence Number**: Random number marking first byte of data.
- **Acknowledgement Number**: Confirms received packets by incrementing sequence.
- **Checksum**: Confirms data hasn't been altered.
- **Data**: Actual file content being sent.
- **Flags**: Indicate how packets are handled during transmission.

---

### 🤝 Three-Way Handshake Steps
1. **SYN** (Client → Server): Initiates connection.
2. **SYN/ACK** (Server → Client): Acknowledges and synchronizes.
3. **ACK** (Client → Server): Final confirmation, connection established.
4. **DATA**: Transmission begins.
5. **FIN**: Gracefully ends the connection.
6. **RST**: Abrupt termination due to error or fault.

**Example Sequence:**
- Client ISN: 0  
- Server ISN: 5000  
- Client ACK: 5001  
- Client sends data starting at sequence 1 (0+1)

---

## 🔚 TCP Connection Termination
- TCP ends a connection when both parties have sent and acknowledged all data.
- Initiated with a **FIN** packet; acknowledged by the receiving device.
- Closes to free up system resources.

---

## 🚀 UDP/IP (User Datagram Protocol)

### ⚡ UDP Overview
- Stateless and connectionless.
- No three-way handshake; data is sent without checking delivery.
- Used where **speed** is prioritized over **reliability** (e.g., video streaming, voice chat).

### ✅ Advantages of UDP
- Faster than TCP.
- No need to maintain a connection.
- Less overhead.

### ⚠️ Disadvantages of UDP
- No delivery confirmation.
- No ordering or integrity checks.
- Poor performance over unstable networks.

---

### 📦 UDP Packet Headers
- **Time to Live (TTL)**: Expiry limit.
- **Source/Destination Address**: IPs of sender/receiver.
- **Source Port**: Random open port of sender.
- **Destination Port**: Defined port of the service (e.g., 80).
- **Data**: Content being transmitted.

---

## ⚓ Ports 101

### 🛳️ What Are Ports?
- Numerical identifiers (0–65535) used to manage connections and services.
- Ports are like docking bays; specific services only accept traffic on specific ports.
- **Standard Ports (0–1024)** are predefined for common services.

### 🔑 Common Protocols & Ports
| Protocol | Port | Description |
|---------|------|-------------|
| FTP     | 21   | File Transfer Protocol |
| SSH     | 22   | Secure remote login (text-based) |
| HTTP    | 80   | Web browser access (unencrypted) |
| SMB     | 445  | File and printer sharing |
| HTTPS   | 443  | Encrypted web access |
| RDP     | 3389 | Remote Desktop Protocol |

> 💡 You can use a different port by specifying it after a colon:  
> Example: `http://example.com:8080`

## Extending Your Network

### Port Forwarding
- Connects applications and services to the internet.
- Opens specific ports on a network.
- Configured at the **router** level.

---

### Firewall
- A device (hardware or software) that controls what traffic is allowed to **enter** or **exit** the network.
- Functions like **border security** for the network.
- Firewall rules can be configured based on:
  - Where the traffic is going
  - Which port it's using
  - What protocol it's using

- Firewalls inspect **packets** to make decisions.
- Can be implemented via hardware or software.
- Categories range from 2 to 5 types.

#### Firewall Categories

**Stateful Firewall**
- Determines behavior based on the **entire connection**, not just individual packets.
- Uses more resources.
- Can block an entire device if a bad connection is detected.

**Stateless Firewall**
- Uses **static rules** to allow or deny individual packets.
- More lightweight than stateful firewalls.
- Not as adaptive—only as effective as the rules in place.
- Useful against high-volume traffic from known sources (e.g., **DDoS attacks**).

---

### Virtual Private Network (VPN)
- Allows devices on separate networks to communicate securely by creating a **dedicated tunnel** over the internet.
- Creates a **private network** across public infrastructure.

#### Benefits of VPNs
- Connects networks across different geographic locations.
- Provides **privacy** and **anonymity**.

#### VPN Technologies

**PPP (Point-to-Point Protocol)**
- Uses **PPTP** for authentication and data encryption.

**PPTP (Point-to-Point Tunneling Protocol)**
- Allows PPP data to travel outside a local network.
- Easy to set up and widely supported.
- Weak encryption compared to modern alternatives.

**IPSec (Internet Protocol Security)**
- Encrypts data using the IP framework.
- Strong encryption and widely supported.
- More difficult to configure.

---

## LAN Networking Devices

### Router
- Connects multiple networks using **routing protocols**.
- Operates at **Layer 3 (Network Layer)** of the OSI model.
- Typically includes an interactive admin interface.
- Used for setting up:
  - Port forwarding
  - Firewall rules

- Determines best path based on:
  - Shortest distance
  - Reliability
  - Speed of transmission medium

---

### Switch
- Dedicated device that connects multiple devices within a local network.
- Operates at **Layer 2 or Layer 3** of the OSI model.

**Layer 2 Switch**
- Works only at the Data Link Layer.
- Uses **MAC addresses** to forward **frames**.

**Layer 3 Switch**
- Combines functionality of a switch and a router.
- Routes **packets** using **IP addresses**.
- Also switches **frames** like a Layer 2 switch.

---

### VLAN (Virtual Local Area Network)
- Allows for virtual segmentation of devices within a network.
- All devices can still access the internet.
- Enhances **security and control** by applying rules on:
  - Which devices can communicate with each other
  - Examples: isolating departments within a business

---


