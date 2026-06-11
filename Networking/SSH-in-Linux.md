# SSH (Secure Shell) in Linux

## Introduction

SSH (Secure Shell) is a secure network protocol used to remotely access and manage Linux servers over a network.

It allows administrators to:

* Log in to remote systems
* Execute commands remotely
* Transfer files securely
* Manage cloud servers
* Configure production environments

SSH is one of the most widely used tools in Linux Administration, DevOps, Cloud Computing, and Cybersecurity.

---

# What is SSH?

SSH stands for:

```text
Secure Shell
```

SSH provides:

* Authentication
* Encryption
* Secure Communication

Without SSH:

```text
Client → Plain Text → Server
```

With SSH:

```text
Client → Encrypted Connection → Server
```

---

# Why SSH is Important

System administrators use SSH to:

* Access remote servers
* Manage Linux machines
* Configure services
* Troubleshoot systems
* Deploy applications

Example:

```text
Laptop
   │
   ▼
SSH Connection
   │
   ▼
Linux Server
```

---

# SSH Architecture

SSH follows a Client-Server model.

```text
SSH Client
      │
      ▼
Encrypted Connection
      │
      ▼
SSH Server
```

Examples:

| Component  | Example     |
| ---------- | ----------- |
| SSH Client | ssh command |
| SSH Server | sshd daemon |

---

# Default SSH Port

SSH uses:

```text
Port 22
```

Check SSH Port:

```bash
sudo ss -tulpn | grep ssh
```

---

# Installing SSH

## Ubuntu/Debian

```bash
sudo apt update
sudo apt install openssh-server
```

---

## RHEL/CentOS

```bash
sudo yum install openssh-server
```

---

# Check SSH Service Status

```bash
systemctl status ssh
```

or

```bash
systemctl status sshd
```

Output:

```text
active (running)
```

---

# Start SSH Service

```bash
sudo systemctl start ssh
```

---

# Enable SSH at Boot

```bash
sudo systemctl enable ssh
```

---

# Restart SSH Service

```bash
sudo systemctl restart ssh
```

---

# Connecting to a Remote Server

Basic Syntax:

```bash
ssh username@server_ip
```

Example:

```bash
ssh ubuntu@192.168.1.100
```

Output:

```text
Password:
```

After successful login:

```text
ubuntu@server:~$
```

---

# Connecting Using Hostname

```bash
ssh user@server01
```

Example:

```bash
ssh admin@webserver
```

---

# Verify Remote Login

Check hostname:

```bash
hostname
```

Check IP:

```bash
ip a
```

---

# SSH Key Authentication

SSH supports passwordless authentication using public and private keys.

Benefits:

* More secure
* Faster login
* Preferred in production

---

# Generate SSH Key Pair

```bash
ssh-keygen
```

Output:

```text
id_rsa
id_rsa.pub
```

Files:

| File       | Purpose     |
| ---------- | ----------- |
| id_rsa     | Private Key |
| id_rsa.pub | Public Key  |

---

# Copy Public Key to Server

```bash
ssh-copy-id user@server_ip
```

Example:

```bash
ssh-copy-id ubuntu@192.168.1.100
```

---

# Login Using SSH Key

```bash
ssh ubuntu@192.168.1.100
```

No password required.

---

# Important SSH Files

## Client Configuration

```text
~/.ssh/config
```

---

## Private Key

```text
~/.ssh/id_rsa
```

---

## Public Key

```text
~/.ssh/id_rsa.pub
```

---

## Authorized Keys

```text
~/.ssh/authorized_keys
```

Contains public keys allowed to access the server.

---

# SSH Configuration File

Server Configuration:

```text
/etc/ssh/sshd_config
```

View:

```bash
sudo nano /etc/ssh/sshd_config
```

---

# Common SSH Configuration Options

## Change Port

Default:

```text
Port 22
```

Change to:

```text
Port 2222
```

Restart SSH:

```bash
sudo systemctl restart ssh
```

---

## Disable Root Login

```text
PermitRootLogin no
```

Recommended for security.

---

## Disable Password Authentication

```text
PasswordAuthentication no
```

Use SSH keys only.

---

# Copy Files Using SCP

SCP = Secure Copy

Copy local file to server:

```bash
scp file.txt user@192.168.1.100:/home/user
```

---

## Download File from Server

```bash
scp user@192.168.1.100:/home/user/file.txt .
```

---

# Transfer Directories

```bash
scp -r project user@192.168.1.100:/home/user
```

---

# Common SSH Commands

## Connect to Server

```bash
ssh user@server_ip
```

---

## Connect Using Port

```bash
ssh -p 2222 user@server_ip
```

---

## Generate Key Pair

```bash
ssh-keygen
```

---

## Copy Key

```bash
ssh-copy-id user@server_ip
```

---

## Secure Copy

```bash
scp file.txt user@server_ip:/home/user
```

---

# Troubleshooting SSH

## Check Service

```bash
systemctl status ssh
```

---

## Check Port

```bash
ss -tulpn | grep ssh
```

---

## Test Connectivity

```bash
ping server_ip
```

---

## Check Firewall

```bash
sudo ufw status
```

or

```bash
sudo firewall-cmd --list-all
```

---

# Real-Life Scenario

Suppose a company hosts a web application on a cloud server.

Administrator workflow:

```text
Laptop
   │
   ▼
SSH Login
   │
   ▼
Linux Cloud Server
   │
   ▼
Update Application
   │
   ▼
Restart Services
```

SSH enables secure management without physical access to the server.

---

# Interview Questions

## Basic

1. What is SSH?
2. What is the default SSH port?
3. What is the purpose of SSH?

---

## Intermediate

4. What is sshd?
5. Difference between SSH and Telnet?
6. How do you generate SSH keys?
7. What is SSH key authentication?

---

## Advanced

8. Explain SSH architecture.
9. How would you secure an SSH server?
10. What is the purpose of authorized_keys?
11. How do you transfer files using SSH?
12. How would you troubleshoot SSH connection failures?

---

# Viva Questions

### Q: What is SSH?

**Answer:**

SSH (Secure Shell) is a secure protocol used to remotely access and manage Linux systems over encrypted network connections.

---

### Q: What is the default SSH port?

**Answer:**

SSH uses TCP Port 22 by default.

---

### Q: Why is SSH preferred over Telnet?

**Answer:**

SSH encrypts all communication, while Telnet sends data in plain text, making SSH much more secure.

---

### Q: What is the difference between a public key and a private key?

**Answer:**

The public key is shared with servers and stored in `authorized_keys`, while the private key remains secret on the client system and is used for authentication.

---

# Summary

SSH (Secure Shell) is the standard tool for secure remote administration of Linux systems. It provides encrypted communication, secure authentication, remote command execution, and file transfer capabilities. SSH is an essential skill for Linux Administrators, DevOps Engineers, Cloud Engineers, and Cybersecurity Professionals.
