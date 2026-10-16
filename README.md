# Department Network Design — Cisco Packet Tracer

A networking fundamentals project demonstrating IPv4 subnetting, network topology design, and interdepartmental communication using Cisco Packet Tracer.

This project connects two departments—**Accounts** and **Delivery**—through a router, allowing devices on separate subnets to communicate. It provides practical experience with IP addressing, subnet masks, default gateways, network devices, and connectivity verification.

## Problem Statement

Design and implement a network in Cisco Packet Tracer to connect the Accounts and Delivery departments using the network address `192.168.40.0`.

Each department must contain at least two PCs. An appropriate number of switches and routers must be used to establish connectivity between the devices.

The network must meet the following requirements:

- Divide the provided network into separate subnets for the two departments.
- Configure appropriate IP addresses and subnet masks for all network interfaces.
- Configure the correct default gateways for end devices.
- Connect all devices using appropriate network cables.
- Establish communication between the Accounts and Delivery departments.
- Verify connectivity between PCs using the `ping` command.

## Project Objectives

- Understand IPv4 addressing and subnetting.
- Divide a network into two departmental subnets.
- Design a network topology using routers, switches, PCs, and printers.
- Configure IP addresses, subnet masks, and default gateways.
- Understand how routers facilitate communication between different networks.
- Test connectivity and interpret ping results.

## Network Topology

The network consists of two departmental LANs connected through a Cisco 1941 router.

Each department contains:
- One Cisco 2960 switch
- Two PCs
- One network printer

The router connects the two departmental networks and enables communication between devices belonging to different subnets.

### Network Design

![Cisco Packet Tracer network topology showing the Accounts and Delivery departments connected through a router](Screenshot%202026-10-16%20at%2012.43.58.png)

### Devices Used

| Device | Quantity | Purpose |
|---|---:|---|
| Cisco 1941 Router | 1 | Routes traffic between the two departmental networks |
| Cisco 2960 Switch | 2 | Connects devices within each department |
| PCs | 4 | End devices used to test network connectivity |
| Printers | 2 | Network peripherals connected to the departmental LANs |

## IPv4 Subnetting

### Given Network Information

| Parameter | Value |
|---|---|
| Network Address | `192.168.40.0` |
| Original Prefix | `/24` |
| Original Subnet Mask | `255.255.255.0` |
| Number of Departments | 2 |
| Required Subnets | 2 |

### Subnet Calculation

The given network is `192.168.40.0/24`, which provides 256 total IP addresses.

Since the network must be divided into two departments, two separate subnets are required.

The number of subnets created by borrowing host bits is calculated using:

\[
\text{Number of Subnets} = 2^n
\]

Where `n` represents the number of bits borrowed from the host portion.

For two subnets:

\[
2^1 = 2
\]

Therefore, **one bit is borrowed from the host portion** to create two subnets.

The original `/24` prefix becomes `/25`.

### New Subnet Mask

The resulting subnet mask is:

`255.255.255.128`

In binary, the subnet mask is:

`11111111.11111111.11111111.10000000`

The block size is calculated as:

\[
\text{Block Size} = 256 - 128 = 128
\]

Each subnet contains 128 total IP addresses, of which 126 are available for host assignment.

### Subnet Addressing Table

The original network is divided into the following two subnets.

| Parameter | Accounts Department | Delivery Department |
|---|---|---|
| Network ID | `192.168.40.0/25` | `192.168.40.128/25` |
| Subnet Mask | `255.255.255.128` | `255.255.255.128` |
| First Usable IP | `192.168.40.1` | `192.168.40.129` |
| Last Usable IP | `192.168.40.126` | `192.168.40.254` |
| Broadcast Address | `192.168.40.127` | `192.168.40.255` |
| Total Addresses | 128 | 128 |
| Usable Host Addresses | 126 | 126 |

### Subnet Allocation

**Subnet 1 — Accounts Department**

- Network ID: `192.168.40.0`
- Subnet Mask: `255.255.255.128`
- Usable Host Range: `192.168.40.1 – 192.168.40.126`
- Broadcast Address: `192.168.40.127`

**Subnet 2 — Delivery Department**

- Network ID: `192.168.40.128`
- Subnet Mask: `255.255.255.128`
- Usable Host Range: `192.168.40.129 – 192.168.40.254`
- Broadcast Address: `192.168.40.255`

Each department uses its own subnet, while the router provides the Layer 3 connectivity required for communication between them.

> **Note:** The addresses above represent the available subnet ranges. Each PC, printer, and router interface must be assigned a unique usable IP address. End devices must use the IP address of their local router interface as their default gateway.

## Implementation

The network was designed and tested using Cisco Packet Tracer.

### 1. Network Topology Setup

The following devices were added to the workspace:

- One Cisco 1941 router
- Two Cisco 2960 switches
- Four PCs
- Two printers

The devices were arranged into two departmental networks: Accounts and Delivery.

### 2. Device Connectivity

Each department's PCs and printer were connected to its respective switch.

The two switches were connected to separate interfaces on the router, allowing the router to forward traffic between the departmental subnets.

Appropriate Ethernet connections were used to establish connectivity between the devices.

### 3. IP Addressing

The network was divided into two `/25` subnets using the subnet mask:

`255.255.255.128`

Devices in the Accounts department use addresses from:

`192.168.40.0/25`

Devices in the Delivery department use addresses from:

`192.168.40.128/25`

Each device must have a unique IP address within its subnet.

### 4. Default Gateway Configuration

The default gateway on each end device must point to the router interface belonging to its respective subnet.

This allows devices to forward traffic destined for a different subnet to the router.

### 5. Connectivity Testing

The `ping` command was used to test connectivity between devices on different departmental networks.

A PC in the Accounts department was used to ping the destination address:

`192.168.40.130`

This address belongs to the Delivery subnet.

## Connectivity Verification

The following screenshot shows the ping test performed from PC0 to `192.168.40.130`.

![Cisco Packet Tracer command prompt showing ping results for 192.168.40.130](Screenshot%202026-10-16%20at%2012.44.07.png)

### Test Results

The initial ping attempt produced the following results:

- Packets sent: 4
- Packets received: 3
- Packets lost: 1
- Packet loss: 25%

A second ping attempt produced:

- Packets sent: 4
- Packets received: 4
- Packets lost: 0
- Packet loss: 0%

### Analysis

The second ping test achieved **100% successful packet delivery**, demonstrating IP connectivity between the source PC and the destination address.

The initial packet loss may occur when Address Resolution Protocol (ARP) resolves a destination's Layer 2 address or when network connectivity is being established. However, the screenshot alone does not confirm the exact cause of the initial timeout.

The successful second test provides evidence that the destination was reachable during that test.

## Skills Practiced

Through this project, I gained practical experience with:

- **IPv4 Addressing:** Understanding network addresses, host addresses, and broadcast addresses.
- **Subnetting:** Dividing a `/24` network into two `/25` subnets.
- **CIDR Notation:** Understanding prefix lengths and their relationship to subnet masks.
- **Network Topology Design:** Building a departmental network in Cisco Packet Tracer.
- **Routing Fundamentals:** Understanding how a router enables communication between different IP networks.
- **IP Configuration:** Working with IP addresses, subnet masks, and default gateways.
- **Connectivity Testing:** Using ICMP ping to verify communication and interpret packet-loss statistics.
- **Basic Troubleshooting:** Observing connectivity test results and considering possible causes of initial packet loss.

## Tools and Technologies

- Cisco Packet Tracer
- IPv4
- Subnetting and CIDR
- Ethernet switching
- IP routing
- ICMP
- ARP

## Repository Structure

```text
department-network-design/
├── README.md
├── Screenshot 2026-10-16 at 12.43.58.png
└── Screenshot 2026-10-16 at 12.44.07.png
```

The screenshots document the network topology and connectivity test.

For a reproducible project, the Cisco Packet Tracer `.pkt` file can also be added to the repository so that others can open the simulation and inspect the configuration.

## Learning Outcome

This project demonstrates the application of IPv4 subnetting to a small departmental network.

By dividing `192.168.40.0/24` into two `/25` subnets, the Accounts and Delivery departments can operate on separate IP networks while communicating through a router.

The project provides a foundation in network addressing, subnet design, routing concepts, device connectivity, and basic network troubleshooting.

These networking fundamentals are important building blocks for further study in cybersecurity, network security, and infrastructure administration.
