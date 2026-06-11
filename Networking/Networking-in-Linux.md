# Networking in Linux

## Introduction

Networking is one of the most important aspects of Linux System Administration. It enables communication between computers, servers, devices, and services over local and global networks.

Linux provides powerful networking tools that help administrators configure, monitor, troubleshoot, and secure network connections.

Networking skills are essential for:

* Linux Administrators
* DevOps Engineers
* Cloud Engineers
* System Engineers
* Cybersecurity Professionals

---

# What is Networking?

Networking is the process of connecting two or more devices so they can exchange data and resources.

Example:

```text
Computer A  ←→  Router  ←→  Server
```

Common resources shared over a network:

* Files
* Printers
* Internet Connection
* Databases
* Applications

---

# Types of Networks

## LAN (Local Area Network)

A network within a small geographical area.

Examples:

* Home Network
* School Network
* Office Network

```text
PC1 ── Switch ── PC2
        │
        └── Server
```

---

## WAN (Wide Area Network)

Connects multiple LANs across large distances.

Example:

```text
Office Delhi
      │
      ▼
   Internet
      ▲
      │
Office Mumbai
```

---

## MAN (Metropolitan Area Network)

Covers a city or metropolitan region.

Example:

```text
City-wide ISP Network
```

---

# IP Address

An IP Address uniquely identifies a device on a network.

Example:

```text
192.168.1.10
```

IPv4 Format:

```text
192.168.1.10
```

IPv6 Format:

```text
2001:db8::1
```

---

# Public vs Private IP

| Type       | Example         |
| ---------- | --------------- |
| Private IP | 192.168.1.10    |
| Public IP  | Assigned by ISP |

Private IP ranges:

```text
10.0.0.0 – 10.255.255.255

172.16.0.0 – 172.31.255.255

192.168.0.0 – 192.168.255.255
```

---

# Hostname

A hostname is the name assigned to a system.

Check hostname:

```bash
hostname
```

Example:

```text
server01
```

---

# Check IP Address

Modern Method:

```bash
ip addr show
```

Shortcut:

```bash
ip a
```

Output:

```text
192.168.1.10/24
```

---

# Display Network Interfaces

```bash
ip link show
```

Output:

```text
eth0
lo
wlan0
```

---

# Understanding Network Interfaces

| Interface | Purpose            |
| --------- | ------------------ |
| lo        | Loopback Interface |
| eth0      | Ethernet           |
| wlan0     | Wireless           |
| ens33     | VMware Interface   |

---

# Loopback Interface

Loopback address:

```text
127.0.0.1
```

Used for:

* Local testing
* Internal communication

Test:

```bash
ping 127.0.0.1
```

---

# Configure IP Address

Temporary Configuration:

```bash
sudo ip addr add 192.168.1.100/24 dev eth0
```

Verify:

```bash
ip addr show
```

---

# Default Gateway

A gateway connects the local network to external networks.

Check Gateway:

```bash
ip route
```

Output:

```text
default via 192.168.1.1
```

---

# DNS (Domain Name System)

DNS converts domain names into IP addresses.

Example:

```text
google.com
     ↓
142.250.183.14
```

DNS Configuration File:

```bash
cat /etc/resolv.conf
```

Example:

```text
nameserver 8.8.8.8
```

---

# Ping Command

Used to test connectivity.

Syntax:

```bash
ping google.com
```

Output:

```text
64 bytes from google.com
```

Interview Favorite ⭐

---

# Traceroute

Shows the path packets take.

Install:

```bash
sudo apt install traceroute
```

Use:

```bash
traceroute google.com
```

---

# Netstat Command

Displays network information.

Show Listening Ports:

```bash
netstat -tuln
```

Options:

| Option | Meaning   |
| ------ | --------- |
| t      | TCP       |
| u      | UDP       |
| l      | Listening |
| n      | Numeric   |

---

# SS Command

Modern replacement for netstat.

Show Listening Ports:

```bash
ss -tuln
```

---

# Check Open Ports

```bash
ss -tulpn
```

Output:

```text
80/tcp
22/tcp
```

---

# Hostname Resolution

Check DNS Resolution:

```bash
nslookup google.com
```

Output:

```text
Address: 142.250.x.x
```

---

# Download Web Content

```bash
curl https://google.com
```

---

# Check HTTP Headers

```bash
curl -I https://google.com
```

---

# Check Connectivity

```bash
ping 8.8.8.8
```

If successful:

```text
Network is reachable
```

---

# View Routing Table

```bash
ip route show
```

Example:

```text
default via 192.168.1.1 dev eth0
```

---

# Networking Troubleshooting Workflow

```text
User Reports Issue
        │
        ▼
Check IP Address
        │
        ▼
Check Gateway
        │
        ▼
Check DNS
        │
        ▼
Ping Remote Host
        │
        ▼
Check Open Ports
        │
        ▼
Resolve Issue
```

---

# Most Important Commands

```bash
hostname

ip a

ip link show

ip route

ping google.com

ss -tuln

nslookup google.com

curl https://google.com
```

---

# Interview Questions

## Basic

1. What is networking?
2. What is an IP address?
3. Difference between IPv4 and IPv6?
4. What is a hostname?
5. What is DNS?

---

## Intermediate

6. What is a gateway?
7. What is a loopback address?
8. Difference between ping and traceroute?
9. How do you check open ports?
10. What is a network interface?

---

## Advanced

11. Explain the networking troubleshooting process.
12. How does DNS resolution work?
13. Explain routing in Linux.
14. Difference between netstat and ss?
15. How would you troubleshoot a server that cannot access the internet?

---

# Viva Answer

### Q: How do you troubleshoot a network issue in Linux?

**Answer:**

First check the IP address using `ip a`, verify the gateway using `ip route`, confirm DNS settings in `/etc/resolv.conf`, test connectivity using `ping`, verify open ports using `ss -tuln`, and use traceroute if required to identify where connectivity is failing.

---

# Summary

Networking is a core Linux administration skill. Commands such as `ip`, `ping`, `ss`, `nslookup`, `curl`, and `traceroute` help administrators configure, monitor, and troubleshoot network connections. A strong understanding of networking concepts is essential for Linux Administration, DevOps, Cloud Computing, and Cybersecurity.

