# Network Troubleshooting in Linux

## Introduction

Network troubleshooting is the process of identifying, diagnosing, and resolving network-related issues in Linux systems.

Every Linux Administrator, DevOps Engineer, Cloud Engineer, and System Administrator must know how to troubleshoot:

* Internet connectivity issues
* DNS failures
* Routing problems
* SSH connection failures
* Service availability issues
* Firewall-related issues

A structured troubleshooting approach helps quickly identify and resolve problems.

---

# Network Troubleshooting Workflow

Always follow this order:

```text
Problem Reported
       │
       ▼
Check Network Interface
       │
       ▼
Check IP Address
       │
       ▼
Check Gateway
       │
       ▼
Check Connectivity
       │
       ▼
Check DNS
       │
       ▼
Check Ports
       │
       ▼
Check Firewall
       │
       ▼
Resolve Issue
```

---

# Step 1: Check Network Interfaces

Display interfaces:

```bash
ip link show
```

Output:

```text
lo
eth0
ens33
wlan0
```

Check interface status:

```bash
ip a
```

Look for:

```text
UP
DOWN
```

If interface is down:

```bash
sudo ip link set eth0 up
```

---

# Step 2: Check IP Address

View assigned IP:

```bash
ip addr show
```

or

```bash
ip a
```

Example:

```text
192.168.1.100/24
```

Interview Favorite ⭐

---

# Step 3: Check Routing Table

Display routes:

```bash
ip route
```

Output:

```text
default via 192.168.1.1 dev eth0
```

Verify:

* Default gateway exists
* Correct network routes exist

---

# Step 4: Test Local Connectivity

Test loopback interface:

```bash
ping 127.0.0.1
```

Expected:

```text
64 bytes from 127.0.0.1
```

If this fails:

```text
TCP/IP stack issue
```

---

# Step 5: Test Network Connectivity

Ping gateway:

```bash
ping 192.168.1.1
```

Successful:

```text
Gateway reachable
```

Failure:

```text
Network issue
```

---

# Step 6: Test Internet Connectivity

Ping public DNS:

```bash
ping 8.8.8.8
```

If successful:

```text
Internet connectivity exists
```

If failed:

```text
Routing issue
Gateway issue
ISP issue
```

---

# Step 7: Test DNS Resolution

Ping domain:

```bash
ping google.com
```

If:

```text
ping 8.8.8.8 works
```

but

```text
ping google.com fails
```

Then:

```text
DNS problem
```

---

# Step 8: Check DNS Configuration

View DNS servers:

```bash
cat /etc/resolv.conf
```

Example:

```text
nameserver 8.8.8.8
nameserver 1.1.1.1
```

---

# Step 9: Verify DNS Lookup

Using nslookup:

```bash
nslookup google.com
```

---

Using dig:

```bash
dig google.com
```

---

Using host:

```bash
host google.com
```

---

# Step 10: Check Open Ports

Display listening ports:

```bash
ss -tuln
```

Example:

```text
22/tcp
80/tcp
443/tcp
```

---

Display process information:

```bash
ss -tulpn
```

---

# Step 11: Check Running Services

Example:

```bash
systemctl status ssh
```

or

```bash
systemctl status nginx
```

Output:

```text
active (running)
```

---

# Step 12: Check Firewall

Ubuntu:

```bash
sudo ufw status
```

---

RHEL/CentOS:

```bash
sudo firewall-cmd --list-all
```

---

Check iptables:

```bash
sudo iptables -L
```

---

# Step 13: Trace Network Path

Install:

```bash
sudo apt install traceroute
```

Run:

```bash
traceroute google.com
```

Output:

```text
Hop 1
Hop 2
Hop 3
```

Shows packet path.

---

# Step 14: Verify DNS Resolution Path

```bash
dig google.com
```

Shows:

* DNS Server
* Response Time
* IP Address

---

# Step 15: Check Active Connections

```bash
ss -tun
```

Displays:

```text
TCP Connections
UDP Connections
```

---

# Step 16: Monitor Network Traffic

```bash
sudo tcpdump
```

Capture traffic:

```bash
sudo tcpdump -i eth0
```

Capture DNS traffic:

```bash
sudo tcpdump port 53
```

Capture HTTP traffic:

```bash
sudo tcpdump port 80
```

Advanced Interview Topic ⭐

---

# Step 17: Test Remote Port Access

Using telnet:

```bash
telnet google.com 80
```

or

```bash
nc -zv google.com 80
```

Output:

```text
Connection successful
```

---

# Most Important Troubleshooting Commands

## Interface Commands

```bash
ip a

ip link show
```

---

## Routing Commands

```bash
ip route
```

---

## Connectivity Commands

```bash
ping 127.0.0.1

ping 192.168.1.1

ping 8.8.8.8

ping google.com
```

---

## DNS Commands

```bash
cat /etc/resolv.conf

nslookup google.com

dig google.com

host google.com
```

---

## Port Commands

```bash
ss -tuln

ss -tulpn
```

---

## Service Commands

```bash
systemctl status ssh

systemctl status nginx
```

---

## Firewall Commands

```bash
ufw status

firewall-cmd --list-all

iptables -L
```

---

## Advanced Commands

```bash
traceroute google.com

tcpdump

nc -zv google.com 80
```

---

# Real-Life Troubleshooting Scenario

## Problem

User reports:

```text
Internet is not working.
```

### Step 1

Check IP:

```bash
ip a
```

---

### Step 2

Check Gateway:

```bash
ip route
```

---

### Step 3

Ping Gateway:

```bash
ping 192.168.1.1
```

---

### Step 4

Ping Public DNS:

```bash
ping 8.8.8.8
```

---

### Step 5

Ping Domain:

```bash
ping google.com
```

---

### Step 6

Check DNS:

```bash
cat /etc/resolv.conf
```

---

### Step 7

Verify DNS:

```bash
nslookup google.com
```

---

### Step 8

Resolve issue.

---

# Common Problems and Solutions

| Problem                | Solution                       |
| ---------------------- | ------------------------------ |
| No IP Address          | Check DHCP or configure IP     |
| Gateway Unreachable    | Verify routing                 |
| Ping Fails             | Check connectivity             |
| DNS Failure            | Check resolv.conf              |
| SSH Not Working        | Check ssh service and port 22  |
| Website Not Accessible | Check web service and firewall |
| Port Closed            | Verify service status          |

---

# Interview Questions

## Basic

1. What is network troubleshooting?
2. How do you check your IP address?
3. How do you verify DNS resolution?

---

## Intermediate

4. Difference between pinging IP and domain?
5. How do you check routing?
6. How do you verify open ports?

---

## Advanced

7. Explain your troubleshooting workflow.
8. How would you troubleshoot SSH failure?
9. How would you diagnose DNS problems?
10. Explain tcpdump usage.
11. How do you troubleshoot a web server that is unreachable?

---

# Viva Questions

### Q: A server can ping 8.8.8.8 but cannot ping google.com. What is the issue?

**Answer:**

Internet connectivity exists, but DNS resolution is failing. Check:

```bash
cat /etc/resolv.conf
nslookup google.com
```

---

### Q: How do you check listening ports?

**Answer:**

```bash
ss -tuln
```

---

### Q: Which command shows routing information?

**Answer:**

```bash
ip route
```

---

### Q: How do you verify SSH service status?

**Answer:**

```bash
systemctl status ssh
```

or

```bash
systemctl status sshd
```

---

# Summary

Network troubleshooting is a critical Linux administration skill. Commands such as `ip`, `ping`, `ss`, `dig`, `nslookup`, `traceroute`, `tcpdump`, and `systemctl` help administrators quickly diagnose and resolve network issues. A structured troubleshooting workflow significantly reduces downtime and improves system reliability.
