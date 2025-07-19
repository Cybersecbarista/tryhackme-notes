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
