# TCP vs UDP in Linux Networking

## Introduction

TCP (Transmission Control Protocol) and UDP (User Datagram Protocol) are the two primary transport layer protocols used in computer networking.

Both protocols operate at the **Transport Layer (Layer 4)** of the OSI Model and are responsible for communication between applications over a network.

Understanding the differences between TCP and UDP is essential for:

* Linux Administration
* DevOps Engineering
* Cloud Computing
* Networking
* Cybersecurity

---

# Where TCP and UDP Fit

```text
Application Layer
       │
       ▼
Transport Layer
   ┌───────┐
   │ TCP   │
   │ UDP   │
   └───────┘
       │
       ▼
Network Layer (IP)
       │
       ▼
Physical Network
```

---

# What is TCP?

TCP stands for:

```text
Transmission Control Protocol
```

TCP is a **connection-oriented protocol** that ensures reliable data delivery.

Features:

* Reliable communication
* Error checking
* Packet ordering
* Data retransmission
* Flow control

---

# TCP Communication Process

Before sending data, TCP establishes a connection using the famous:

## Three-Way Handshake

```text
Client                     Server
  │                           │
  │ ------- SYN -----------> │
  │                           │
  │ <----- SYN-ACK ---------- │
  │                           │
  │ ------- ACK -----------> │
  │                           │
Connection Established
```

After this, data transmission begins.

---

# What is UDP?

UDP stands for:

```text
User Datagram Protocol
```

UDP is a **connectionless protocol**.

It sends data without establishing a connection first.

```text
Sender
   │
   ▼
Data Sent
   │
   ▼
Receiver
```

No handshake is performed.

---

# Key Characteristics of TCP

## Reliability

TCP guarantees delivery.

If a packet is lost:

```text
Lost Packet
     │
     ▼
Retransmission
```

---

## Ordered Delivery

Data arrives in the correct order.

Example:

```text
Packet 1
Packet 2
Packet 3
```

Received as:

```text
Packet 1
Packet 2
Packet 3
```

---

## Error Detection

TCP verifies data integrity using checksums.

---

## Flow Control

Prevents a sender from overwhelming a receiver.

---

# Key Characteristics of UDP

## Faster Communication

No connection setup required.

---

## Lower Overhead

Fewer headers and processing.

---

## No Delivery Guarantee

Lost packets are not retransmitted.

---

## No Packet Ordering

Packets may arrive:

```text
Packet 3
Packet 1
Packet 2
```

---

## Best-Effort Delivery

UDP simply sends packets and moves on.

---

# TCP vs UDP Comparison

| Feature         | TCP                 | UDP                    |
| --------------- | ------------------- | ---------------------- |
| Connection Type | Connection-Oriented | Connectionless         |
| Reliability     | Reliable            | Unreliable             |
| Packet Ordering | Guaranteed          | Not Guaranteed         |
| Error Recovery  | Yes                 | No                     |
| Speed           | Slower              | Faster                 |
| Overhead        | Higher              | Lower                  |
| Flow Control    | Yes                 | No                     |
| Handshake       | Three-Way Handshake | None                   |
| Use Cases       | Web, Email, SSH     | Streaming, Gaming, DNS |

---

# Common TCP Applications

## HTTP

```text
Port 80
```

---

## HTTPS

```text
Port 443
```

---

## SSH

```text
Port 22
```

---

## FTP

```text
Port 21
```

---

## SMTP

```text
Port 25
```

---

## MySQL

```text
Port 3306
```

---

# Common UDP Applications

## DNS

```text
Port 53
```

---

## DHCP

```text
Port 67
Port 68
```

---

## TFTP

```text
Port 69
```

---

## SNMP

```text
Port 161
```

---

## Online Gaming

```text
Uses UDP for low latency
```

---

## Video Streaming

```text
YouTube Live
VoIP
Video Calls
```

---

# Why SSH Uses TCP

SSH requires:

* Reliable communication
* Packet ordering
* Secure authentication

Therefore:

```text
SSH → TCP Port 22
```

---

# Why DNS Uses UDP

DNS queries are:

* Small
* Fast
* Simple

Therefore:

```text
DNS → UDP Port 53
```

However, DNS can also use TCP for large responses and zone transfers.

---

# Linux Commands to View TCP Connections

## Show TCP Connections

```bash
ss -t
```

---

## Show Listening TCP Ports

```bash
ss -lt
```

---

## Show TCP Processes

```bash
ss -ltpn
```

---

# Linux Commands to View UDP Connections

## Show UDP Connections

```bash
ss -u
```

---

## Show Listening UDP Ports

```bash
ss -lu
```

---

## Show UDP Processes

```bash
ss -lupn
```

---

# Display Both TCP and UDP

```bash
ss -tuln
```

Output Example:

```text
tcp LISTEN 0 128 *:22
tcp LISTEN 0 128 *:80
udp UNCONN 0 0 *:53
```

Interview Favorite ⭐

---

# Using Netstat

## TCP Ports

```bash
netstat -tln
```

---

## UDP Ports

```bash
netstat -uln
```

---

## All Listening Ports

```bash
netstat -tuln
```

---

# Checking Specific Port

Check SSH:

```bash
ss -tulpn | grep 22
```

---

Check DNS:

```bash
ss -tulpn | grep 53
```

---

# Real-Life Example

## Web Browser

When opening:

```text
https://google.com
```

Browser uses:

```text
TCP Port 443
```

because reliability is required.

---

## Video Streaming

During live streaming:

```text
User → Video Stream
```

UDP is preferred because:

```text
Speed > Perfect Delivery
```

Losing a few frames is acceptable.

---

# TCP Header vs UDP Header

## TCP Header

Contains:

* Source Port
* Destination Port
* Sequence Number
* Acknowledgment Number
* Window Size
* Checksum

More overhead.

---

## UDP Header

Contains:

* Source Port
* Destination Port
* Length
* Checksum

Simpler and smaller.

---

# Most Important Commands

```bash
ss -t

ss -u

ss -lt

ss -lu

ss -tuln

ss -tulpn

netstat -tuln
```

---

# Interview Questions

## Basic

1. What is TCP?
2. What is UDP?
3. Difference between TCP and UDP?
4. Which protocol is faster?

---

## Intermediate

5. What is the TCP three-way handshake?
6. Why is TCP reliable?
7. Why is UDP faster?
8. Which protocol does DNS use?

---

## Advanced

9. Explain TCP connection establishment.
10. Why does SSH use TCP?
11. Why does video streaming use UDP?
12. How do you check TCP and UDP ports in Linux?
13. Explain packet ordering and retransmission.

---

# Viva Questions

### Q: What is the main difference between TCP and UDP?

**Answer:**

TCP is connection-oriented and provides reliable communication, while UDP is connectionless and prioritizes speed over reliability.

---

### Q: Which protocol is used by SSH?

**Answer:**

SSH uses TCP on Port 22.

---

### Q: Which protocol is used by DNS?

**Answer:**

DNS primarily uses UDP on Port 53.

---

### Q: Why is UDP faster than TCP?

**Answer:**

UDP does not perform connection establishment, acknowledgments, retransmissions, or flow control, resulting in lower overhead and faster communication.

---

### Q: Which command displays both TCP and UDP listening ports?

**Answer:**

```bash
ss -tuln
```

---

# Summary

TCP and UDP are the two fundamental transport layer protocols in networking. TCP provides reliable, ordered, and error-checked communication, while UDP provides fast, lightweight, and low-latency communication. Linux administrators frequently use commands such as `ss`, `netstat`, and `tcpdump` to analyze TCP and UDP traffic and troubleshoot network-related issues.
