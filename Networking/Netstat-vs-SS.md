# Netstat vs SS in Linux

## Introduction

Linux administrators frequently need to inspect:

* Open ports
* Active network connections
* Listening services
* TCP/UDP sockets
* Process-to-port mappings

Traditionally, the `netstat` command was used for this purpose. However, modern Linux distributions recommend using the `ss` command because it is faster and more efficient.

Understanding both commands is important for:

* Linux Administration
* DevOps Engineering
* Cloud Computing
* System Administration
* Cybersecurity

---

# What is Netstat?

Netstat stands for:

```text
Network Statistics
```

It is a command-line utility used to display:

* Active connections
* Listening ports
* Routing tables
* Network interfaces
* Network statistics

Example:

```bash
netstat -tuln
```

Output:

```text
tcp   0   0 0.0.0.0:22      0.0.0.0:*     LISTEN
tcp   0   0 0.0.0.0:80      0.0.0.0:*     LISTEN
udp   0   0 0.0.0.0:53      0.0.0.0:*
```

---

# What is SS?

SS stands for:

```text
Socket Statistics
```

It is the modern replacement for netstat.

SS retrieves socket information directly from the Linux kernel, making it:

* Faster
* More accurate
* More efficient

Example:

```bash
ss -tuln
```

Output:

```text
tcp LISTEN 0 128 *:22
tcp LISTEN 0 128 *:80
udp UNCONN 0 0 *:53
```

---

# Why SS Replaced Netstat

Netstat belongs to:

```text
net-tools package
```

which is largely considered legacy software.

Modern Linux systems use:

```text
iproute2 package
```

which provides:

```text
ip
ss
```

commands.

---

# Netstat vs SS Comparison

| Feature        | Netstat        | SS             |
| -------------- | -------------- | -------------- |
| Package        | net-tools      | iproute2       |
| Speed          | Slower         | Faster         |
| Resource Usage | Higher         | Lower          |
| Modern Support | Legacy         | Recommended    |
| Kernel Access  | Indirect       | Direct         |
| Large Systems  | Less Efficient | More Efficient |
| Future Use     | Limited        | Preferred      |

Interview Favorite ⭐

---

# Installation

## Netstat

Ubuntu/Debian:

```bash
sudo apt install net-tools
```

RHEL/CentOS:

```bash
sudo yum install net-tools
```

---

## SS

Already available on most Linux systems.

Verify:

```bash
ss --version
```

---

# Display All Connections

## Netstat

```bash
netstat -a
```

---

## SS

```bash
ss -a
```

---

# Show TCP Connections

## Netstat

```bash
netstat -t
```

---

## SS

```bash
ss -t
```

---

# Show UDP Connections

## Netstat

```bash
netstat -u
```

---

## SS

```bash
ss -u
```

---

# Show Listening Ports

## Netstat

```bash
netstat -l
```

---

## SS

```bash
ss -l
```

---

# Show Listening TCP Ports

## Netstat

```bash
netstat -lt
```

---

## SS

```bash
ss -lt
```

---

# Show Listening UDP Ports

## Netstat

```bash
netstat -lu
```

---

## SS

```bash
ss -lu
```

---

# Display Numeric Addresses

## Netstat

```bash
netstat -n
```

---

## SS

```bash
ss -n
```

---

# Show Process Information

## Netstat

```bash
netstat -tulpn
```

Output:

```text
tcp 0 0 0.0.0.0:22 LISTEN 1234/sshd
```

---

## SS

```bash
ss -tulpn
```

Output:

```text
tcp LISTEN 0 128 *:22 users:(("sshd",pid=1234))
```

---

# Show Routing Table

## Netstat

```bash
netstat -r
```

---

## Modern Alternative

```bash
ip route
```

Recommended.

---

# Display Interface Statistics

## Netstat

```bash
netstat -i
```

---

## Modern Alternative

```bash
ip -s link
```

---

# Most Important SS Commands

## Show All Connections

```bash
ss -a
```

---

## Show TCP Connections

```bash
ss -t
```

---

## Show UDP Connections

```bash
ss -u
```

---

## Show Listening Ports

```bash
ss -l
```

---

## Show Listening TCP Ports

```bash
ss -lt
```

---

## Show Listening UDP Ports

```bash
ss -lu
```

---

## Show Processes Using Ports

```bash
ss -tulpn
```

---

## Filter Specific Port

Check SSH:

```bash
ss -tulpn | grep 22
```

---

Check HTTP:

```bash
ss -tulpn | grep 80
```

---

Check HTTPS:

```bash
ss -tulpn | grep 443
```

---

# Real-Life Examples

## Verify SSH Service

```bash
ss -tulpn | grep 22
```

Expected:

```text
LISTEN *:22
```

---

## Verify Nginx

```bash
ss -tulpn | grep 80
```

Expected:

```text
LISTEN *:80
```

---

## Verify HTTPS

```bash
ss -tulpn | grep 443
```

Expected:

```text
LISTEN *:443
```

---

# Troubleshooting Scenario

## Problem

User reports:

```text
Cannot connect to web server.
```

Administrator checks:

```bash
ss -tulpn | grep 80
```

No output:

```text
Port 80 not listening
```

Check service:

```bash
systemctl status nginx
```

Result:

```text
nginx service stopped
```

Solution:

```bash
sudo systemctl start nginx
```

Verify:

```bash
ss -tulpn | grep 80
```

---

# Netstat to SS Conversion Table

| Netstat        | SS        |
| -------------- | --------- |
| netstat -a     | ss -a     |
| netstat -t     | ss -t     |
| netstat -u     | ss -u     |
| netstat -l     | ss -l     |
| netstat -lt    | ss -lt    |
| netstat -lu    | ss -lu    |
| netstat -n     | ss -n     |
| netstat -tulpn | ss -tulpn |
| netstat -r     | ip route  |

---

# Most Important Commands for Interviews

```bash
ss -a

ss -t

ss -u

ss -l

ss -lt

ss -lu

ss -tulpn

ss -tulpn | grep 22

ss -tulpn | grep 80

ss -tulpn | grep 443

ip route
```

---

# Interview Questions

## Basic

1. What is netstat?
2. What is ss?
3. Why is ss preferred over netstat?

---

## Intermediate

4. How do you display listening ports?
5. How do you identify which process is using a port?
6. How do you view TCP connections?

---

## Advanced

7. Explain why ss is faster than netstat.
8. How would you verify if SSH is listening?
9. How would you troubleshoot a web server using ss?
10. What package provides the ss command?

---

# Viva Questions

### Q: What is the difference between netstat and ss?

**Answer:**

Both display network connections and ports. However, `ss` is faster, consumes fewer resources, and directly retrieves socket information from the Linux kernel, making it the preferred modern tool.

---

### Q: Which command shows all listening ports?

**Answer:**

```bash
ss -l
```

---

### Q: Which command shows the process using a port?

**Answer:**

```bash
ss -tulpn
```

---

### Q: Which package provides netstat?

**Answer:**

```text
net-tools
```

---

### Q: Which package provides ss?

**Answer:**

```text
iproute2
```

---

# Summary

Netstat and SS are Linux networking utilities used to inspect sockets, ports, and connections. While netstat is a legacy tool from the net-tools package, SS is the modern replacement provided by iproute2. Linux administrators should prioritize learning SS because it is faster, more efficient, and widely used in modern Linux environments.
