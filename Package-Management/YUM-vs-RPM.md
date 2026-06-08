# YUM vs RPM

## Introduction

YUM and RPM are both package management tools used in Red Hat-based Linux distributions. Although they are related, they serve different purposes.

**RPM** is a low-level package management system used to install, remove, verify, and query RPM packages.

**YUM** is a high-level package manager that works on top of RPM and provides automatic dependency resolution and repository management.

---

## Full Forms

| Tool | Full Form                  |
| ---- | -------------------------- |
| RPM  | Red Hat Package Manager    |
| YUM  | Yellowdog Updater Modified |

---

## What is RPM?

RPM is the package format and installation engine used by Red Hat-based Linux distributions.

It allows administrators to:

* Install packages
* Remove packages
* Upgrade packages
* Query package information
* Verify package integrity

RPM works directly with `.rpm` files.

### RPM Package Example

```text
nginx-1.24.0.rpm
```

### Install a Package Using RPM

```bash
sudo rpm -ivh nginx.rpm
```

### Remove a Package

```bash
sudo rpm -e nginx
```

### List Installed Packages

```bash
rpm -qa
```

### View Package Information

```bash
rpm -qi nginx
```

---

## What is YUM?

YUM is a package manager that simplifies software installation and management.

YUM automatically:

* Searches repositories
* Downloads packages
* Resolves dependencies
* Installs required libraries
* Updates software

YUM uses RPM internally for actual installation.

### Install a Package Using YUM

```bash
sudo yum install nginx
```

### Update Packages

```bash
sudo yum update
```

### Remove a Package

```bash
sudo yum remove nginx
```

### Search for a Package

```bash
yum search nginx
```

---

## Major Difference

### RPM

When installing software using RPM:

```bash
sudo rpm -ivh nginx.rpm
```

If required dependencies are missing, RPM displays an error:

```text
error: Failed dependencies:
libssl.so is needed by nginx
```

The administrator must manually install all missing dependencies.

---

### YUM

When installing software using YUM:

```bash
sudo yum install nginx
```

YUM automatically:

1. Finds the package
2. Checks dependencies
3. Downloads dependencies
4. Installs everything

No manual dependency management is required.

---

## Detailed Comparison

| Feature                             | RPM                       | YUM                        |
| ----------------------------------- | ------------------------- | -------------------------- |
| Type                                | Low-level package manager | High-level package manager |
| Dependency Resolution               | Manual                    | Automatic                  |
| Repository Support                  | No                        | Yes                        |
| Package Download                    | No                        | Yes                        |
| Software Updates                    | Limited                   | Full support               |
| Ease of Use                         | Moderate                  | Easy                       |
| Works With                          | Local RPM files           | Repositories and RPM files |
| Uses Internet Repositories          | No                        | Yes                        |
| Installs Dependencies Automatically | No                        | Yes                        |
| Uses RPM Internally                 | No                        | Yes                        |

---

## Relationship Between YUM and RPM

YUM is built on top of RPM.

Workflow:

```text
User Request
      │
      ▼
YUM
      │
      ▼
Repository Check
      │
      ▼
Dependency Resolution
      │
      ▼
Download Packages
      │
      ▼
RPM Installation Engine
      │
      ▼
Software Installed
```

Think of RPM as the engine and YUM as the driver.

---

## Real-Life Analogy

Imagine buying a computer.

### RPM

You buy:

* CPU
* RAM
* Motherboard
* Storage

separately and assemble everything yourself.

### YUM

You order a complete computer package.

Everything required is automatically included.

This makes YUM easier and faster.

---

## Advantages of RPM

* Direct package control
* Useful for local installations
* Lightweight
* Detailed package information
* Suitable for advanced administrators

### Disadvantages of RPM

* No automatic dependency resolution
* Manual package management
* More time-consuming

---

## Advantages of YUM

* Automatic dependency handling
* Easy software installation
* Repository support
* System-wide updates
* User-friendly

### Disadvantages of YUM

* Requires repository configuration
* Slightly slower due to dependency checks

---

## Practical Example

### Installing Apache Web Server with RPM

```bash
sudo rpm -ivh httpd.rpm
```

Possible result:

```text
Dependency Error:
libapr.so missing
libssl.so missing
```

Administrator must install these manually.

---

### Installing Apache Web Server with YUM

```bash
sudo yum install httpd
```

YUM automatically:

* Downloads Apache
* Downloads dependencies
* Installs everything
* Configures the package database

---

## Interview Questions

### Basic

1. What is RPM?
2. What is YUM?
3. What is the full form of RPM?
4. What is the full form of YUM?

### Intermediate

5. Why is YUM preferred over RPM?
6. Does RPM handle dependencies automatically?
7. Does YUM use RPM internally?
8. What are repositories?

### Advanced

9. Explain the relationship between RPM and YUM.
10. Compare RPM and YUM with examples.
11. Why is dependency resolution important?
12. Explain the package installation process in YUM.

---

## Viva Answer

**Q: What is the difference between RPM and YUM?**

**Answer:**

RPM is a low-level package management tool used to install and manage RPM packages, while YUM is a high-level package manager that automatically resolves dependencies, downloads packages from repositories, and uses RPM internally to perform installations.

---

## Summary

RPM is the core package management system for Red Hat-based Linux distributions. YUM is a higher-level package manager built on top of RPM that simplifies software installation through repository management and automatic dependency resolution. Therefore, YUM is generally preferred for daily package management tasks.
