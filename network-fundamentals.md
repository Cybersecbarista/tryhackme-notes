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

