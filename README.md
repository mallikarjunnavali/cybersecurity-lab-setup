# 🔐 Cybersecurity & Penetration Testing Lab

> **An isolated multi-OS virtual cybersecurity laboratory for network reconnaissance, vulnerability assessment, penetration-testing practice, packet analysis, and security research.**

![Cybersecurity](https://img.shields.io/badge/Domain-Cybersecurity-red)
![Networking](https://img.shields.io/badge/Networking-VMware%20NAT-blue)
![Kali Linux](https://img.shields.io/badge/Attack%20Platform-Kali%20Linux-557C94)
![Windows](https://img.shields.io/badge/Targets-Windows%207%20%7C%2010%20%7C%2011-blue)
![Android](https://img.shields.io/badge/Target-Android--x86-green)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange)

---

## 📌 Project Overview

This project is a **controlled and isolated penetration-testing laboratory** built using **VMware Workstation**.

The lab contains a Kali Linux attack machine connected to multiple intentionally configured target systems:

* 🐉 Kali Linux — Attacker
* 🤖 Android-x86 — Target
* 🪟 Windows 7 — Target
* 🪟 Windows 10 — Target
* 🪟 Windows 11 — Target

All virtual machines communicate through a custom **VMware VMnet8 NAT network** using the `10.0.0.0/24` subnet.

The environment is designed to provide a safe platform for learning:

* Network reconnaissance
* Port scanning
* Service enumeration
* Vulnerability assessment
* Windows security testing
* Android security testing
* Packet analysis
* Exploitation fundamentals
* Post-exploitation concepts
* Network security monitoring

> ⚠️ **Important:** All security testing in this project is intended only for systems that I own or have explicit authorization to test.

---

# 🎯 Project Objectives

The main objectives of this project are:

* Configure a custom VMware NAT network.
* Build an isolated cybersecurity laboratory.
* Configure static IP addressing across multiple operating systems.
* Deploy Kali Linux as the security-testing platform.
* Deploy multiple Windows versions as vulnerable/assessment targets.
* Deploy Android-x86 as an Android security-testing target.
* Establish communication between attacker and target systems.
* Verify network connectivity.
* Configure Windows ICMP firewall rules.
* Practice reconnaissance and service enumeration.
* Capture and analyze network traffic.
* Create recoverable VM snapshots/baselines.
* Develop practical networking and cybersecurity skills.

---

# 🏗️ Lab Architecture

```text
                         INTERNET
                            │
                            │
                     ┌──────▼──────┐
                     │ VMware NAT  │
                     │  Gateway    │
                     │ 10.0.0.1    │
                     └──────┬──────┘
                            │
                    ┌───────▼────────┐
                    │    VMnet8      │
                    │  10.0.0.0/24   │
                    │   NAT Network   │
                    └───────┬────────┘
                            │
       ┌────────────────────┼────────────────────┐
       │                    │                    │
       ▼                    ▼                    ▼
┌─────────────┐      ┌─────────────┐      ┌─────────────┐
│ Kali Linux  │      │ Windows 7   │      │ Windows 10  │
│ 10.0.0.2    │      │ 10.0.0.7    │      │ 10.0.0.10   │
│  ATTACKER   │      │   TARGET    │      │   TARGET    │
└─────────────┘      └─────────────┘      └─────────────┘
       │
       │
       ├─────────────────────┐
       │                     │
       ▼                     ▼
┌─────────────┐       ┌─────────────┐
│ Android-x86 │       │ Windows 11  │
│ 10.0.0.9    │       │ 10.0.0.16   │
│   TARGET    │       │   TARGET    │
└─────────────┘       └─────────────┘
```

---

# 🌐 Network Configuration

| Device         | Role        |  IP Address | Network |
| -------------- | ----------- | ----------: | ------- |
| VMware Gateway | NAT Gateway |  `10.0.0.1` | VMnet8  |
| Kali Linux     | Attacker    |  `10.0.0.2` | VMnet8  |
| Windows 7      | Target      |  `10.0.0.7` | VMnet8  |
| Android-x86    | Target      |  `10.0.0.9` | VMnet8  |
| Windows 10     | Target      | `10.0.0.10` | VMnet8  |
| Windows 11     | Target      | `10.0.0.16` | VMnet8  |

### Network Parameters

```text
Network        : 10.0.0.0/24
Subnet Mask    : 255.255.255.0
Gateway        : 10.0.0.1
DNS            : 8.8.8.8
Virtual Network: VMnet8
Network Type   : NAT
```

---

# 🧰 Technologies & Tools

## Virtualization

* VMware Workstation
* VMware Virtual Network Editor
* VMnet8 NAT networking

## Attack Platform

* Kali Linux
* Nmap
* Metasploit Framework
* Wireshark
* Netcat
* ADB

## Target Platforms

* Windows 7
* Windows 10
* Windows 11
* Android-x86

## Networking

* IPv4
* NAT
* Static IP addressing
* ICMP
* TCP/IP
* DNS
* Virtual networking

---

# ⚙️ Lab Setup

## 1️⃣ Configure VMware VMnet8

Open:

```text
VMware Workstation
        ↓
Edit
        ↓
Virtual Network Editor
        ↓
VMnet8
```

Configure:

```text
Network Type : NAT
Subnet IP    : 10.0.0.0
Subnet Mask  : 255.255.255.0
Gateway      : 10.0.0.1
```

---

## 2️⃣ Configure VMware Host Adapter

Open:

```text
Win + R
```

Run:

```text
ncpa.cpl
```

Find:

```text
VMware Network Adapter VMnet8
```

Configure IPv4:

```text
IP Address : 10.0.0.1
Subnet     : 255.255.255.0
DNS        : 8.8.8.8
```

---

# 🐉 3️⃣ Kali Linux Configuration

Kali Linux is used as the primary security-testing machine.

Configure the VMware adapter:

```text
Network Adapter
        ↓
Custom
        ↓
VMnet8
```

Kali network configuration:

```text
IP Address : 10.0.0.2
Netmask    : 255.255.255.0
Gateway    : 10.0.0.1
DNS        : 8.8.8.8
```

Verify the interface:

```bash
ip a
```

Check the routing table:

```bash
ip route
```

Expected default route:

```text
default via 10.0.0.1
```

---

# 🪟 4️⃣ Windows Target Configuration

The Windows machines are configured with static addresses.

### Windows 7

```text
IP      : 10.0.0.7
Mask    : 255.255.255.0
Gateway : 10.0.0.1
DNS     : 8.8.8.8
```

### Windows 10

```text
IP      : 10.0.0.10
Mask    : 255.255.255.0
Gateway : 10.0.0.1
DNS     : 8.8.8.8
```

### Windows 11

```text
IP      : 10.0.0.16
Mask    : 255.255.255.0
Gateway : 10.0.0.1
DNS     : 8.8.8.8
```

---

# 🛡️ Enable ICMP on Windows Targets

Windows Firewall may block incoming ICMP Echo Requests.

Run Command Prompt as Administrator:

```cmd
netsh advfirewall firewall add rule name="Allow ICMPv4" protocol=icmpv4:8,any dir=in action=allow
```

This allows the target to respond to IPv4 ping requests.

---

# 🤖 5️⃣ Android-x86 Target

Android-x86 is deployed as a separate virtual machine.

VM configuration:

```text
Guest OS:
Linux → Other Linux 5.x kernel 64-bit
```

Installation:

```text
android-x86_64-9.0-r2.iso
```

Disk:

```text
Filesystem : ext4
Bootloader : GRUB
```

Network:

```text
IP      : 10.0.0.9
Mask    : 255.255.255.0
Gateway : 10.0.0.1
```

---

# 🧪 Network Verification

From Kali Linux:

### Check interface

```bash
ip a
```

### Check gateway

```bash
ping -c 4 10.0.0.1
```

### Check Windows 7

```bash
ping -c 4 10.0.0.7
```

### Check Android

```bash
ping -c 4 10.0.0.9
```

### Check Windows 10

```bash
ping -c 4 10.0.0.10
```

### Check Windows 11

```bash
ping -c 4 10.0.0.16
```

### Check Internet connectivity

```bash
ping -c 4 8.8.8.8
```

### Check DNS

```bash
ping -c 4 google.com
```

---

# 🔎 Reconnaissance & Enumeration

Once the lab is operational, reconnaissance can be performed against the **lab targets only**.

### Host discovery

```bash
nmap -sn 10.0.0.0/24
```

### Basic port scan

```bash
nmap 10.0.0.10
```

### Service enumeration

```bash
nmap -sV 10.0.0.10
```

### Operating-system detection

```bash
sudo nmap -O 10.0.0.10
```

### More detailed lab scan

```bash
sudo nmap -sC -sV 10.0.0.10
```

> Use scanning commands only against systems you own or are explicitly authorized to test.

---

# 📡 Packet Analysis

Wireshark can be used to observe communication between:

```text
Kali
  ↕
VMnet8
  ↕
Target VMs
```

Useful traffic to study:

* ARP
* ICMP
* TCP
* UDP
* DNS
* HTTP
* SMB
* DHCP

Example workflow:

```text
Start Wireshark
      ↓
Select VMnet8 interface
      ↓
Start Capture
      ↓
Generate traffic from Kali
      ↓
Analyze packets
```

Example filters:

```text
icmp
```

```text
arp
```

```text
tcp
```

```text
dns
```

---

# 💥 Security Testing Areas

The laboratory can be used to study:

### Network Reconnaissance

* Host discovery
* Port scanning
* Service identification
* OS detection

### Windows Security

* SMB
* RPC
* Windows services
* Authentication
* Firewall behavior
* Vulnerability assessment

### Android Security

* ADB
* Android services
* Application security
* Shell access
* Network communication

### Exploitation Fundamentals

* Metasploit Framework
* Vulnerability validation
* Controlled payload testing
* Post-exploitation concepts

### Network Monitoring

* Wireshark
* Packet capture
* Protocol analysis
* Traffic investigation

---

# 🐞 Problems Encountered & Solutions

## Problem 1 — Android Booting to `console:/ #`

### Symptom

Android-x86 booted into:

```text
console:/ #
```

instead of the graphical Android environment.

### Cause

The installation ISO was still connected to the virtual CD/DVD drive.

### Solution

Open:

```text
VM Settings
    ↓
CD/DVD
```

Disable:

```text
Connected
Connect at power on
```

Then remove/unmount the ISO and restart the VM.

---

## Problem 2 — Windows Target Not Responding to Ping

### Symptom

From Kali:

```bash
ping 10.0.0.10
```

returned:

```text
100% packet loss
```

### Cause

Windows Defender Firewall was blocking inbound ICMP Echo Requests.

### Solution

Run:

```cmd
netsh advfirewall firewall add rule name="Allow ICMPv4" protocol=icmpv4:8,any dir=in action=allow
```

Then test again from Kali.

---

# 💾 VM Recovery & Snapshots

Before performing security testing:

1. Shut down the VM.
2. Create a VMware snapshot.
3. Give it a meaningful name.

Example:

```text
Windows10-Clean-Baseline
Windows7-Clean-Baseline
Windows11-Clean-Baseline
Android-Clean-Baseline
Kali-Clean-Baseline
```

This allows the laboratory to be restored after experiments.

---

# 📸 Project Screenshots

Screenshots can be added to the repository using:

```text
screenshots/
├── vmware-network-editor.png
├── kali-ip-config.png
├── network-topology.png
├── windows10-ip-config.png
├── windows11-ip-config.png
├── windows7-ip-config.png
├── android-network.png
├── ping-tests.png
├── nmap-scan.png
└── wireshark-capture.png
```

Then display them in this README:

```markdown
## VMware VMnet8 Configuration

![VMnet8 Configuration](screenshots/vmware-network-editor.png)

## Kali Network Configuration

![Kali Network](screenshots/kali-ip-config.png)

## Network Verification

![Ping Tests](screenshots/ping-tests.png)

## Nmap Enumeration

![Nmap Scan](screenshots/nmap-scan.png)

## Wireshark Packet Capture

![Wireshark](screenshots/wireshark-capture.png)
```

---

# 📊 Current Lab Status

| Component      |          IP |     Status    |
| -------------- | ----------: | :-----------: |
| VMware Gateway |  `10.0.0.1` |   🟢 Active   |
| Kali Linux     |  `10.0.0.2` |   🟢 Active   |
| Windows 7      |  `10.0.0.7` | 🟢 Configured |
| Android-x86    |  `10.0.0.9` | 🟢 Configured |
| Windows 10     | `10.0.0.10` | 🟢 Configured |
| Windows 11     | `10.0.0.16` | 🟢 Configured |
| Internet/NAT   |   `8.8.8.8` |  🟢 Verified  |

---

# 📚 Useful Official Resources

## Virtualization

* VMware Workstation — [VMware Official Website](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion?utm_source=chatgpt.com)

## Kali Linux

* [Kali Linux Official Website](https://www.kali.org/?utm_source=chatgpt.com)
* [Kali Linux Documentation](https://www.kali.org/docs/?utm_source=chatgpt.com)
* [Kali Tools Documentation](https://www.kali.org/tools/?utm_source=chatgpt.com)

## Nmap

* [Nmap Official Website](https://nmap.org/?utm_source=chatgpt.com)
* [Nmap Documentation](https://nmap.org/book/man.html?utm_source=chatgpt.com)

## Wireshark

* [Wireshark Official Website](https://www.wireshark.org/?utm_source=chatgpt.com)
* [Wireshark Documentation](https://www.wireshark.org/docs/?utm_source=chatgpt.com)

## Metasploit

* [Metasploit Official Website](https://www.metasploit.com/?utm_source=chatgpt.com)
* [Metasploit Documentation](https://docs.metasploit.com/?utm_source=chatgpt.com)

## Android-x86

* [Android-x86 Official Website](https://www.android-x86.org/?utm_source=chatgpt.com)

## Security Learning

* [TryHackMe](https://tryhackme.com/?utm_source=chatgpt.com)
* [OWASP](https://owasp.org/?utm_source=chatgpt.com)
* [MITRE ATT&CK](https://attack.mitre.org/?utm_source=chatgpt.com)
* [CVE.org](https://www.cve.org/?utm_source=chatgpt.com)
* [NIST Cybersecurity Resources](https://www.nist.gov/cybersecurity?utm_source=chatgpt.com)

---

# 📁 Suggested Repository Structure

```text
cybersecurity-pentest-lab/
│
├── README.md
│
├── screenshots/
│   ├── vmware-network-editor.png
│   ├── network-topology.png
│   ├── kali-ip-config.png
│   ├── windows7-ip-config.png
│   ├── windows10-ip-config.png
│   ├── windows11-ip-config.png
│   ├── android-network.png
│   ├── ping-tests.png
│   ├── nmap-scan.png
│   └── wireshark-capture.png
│
├── documentation/
│   ├── network-configuration.md
│   ├── reconnaissance.md
│   ├── packet-analysis.md
│   └── troubleshooting.md
│
├── scans/
│   └── README.md
│
└── LICENSE
```

---

# 🚀 Future Tasks

The next phase of the project will focus on:

* [ ] Perform complete network reconnaissance.
* [ ] Identify open ports on each target.
* [ ] Enumerate running services.
* [ ] Analyze SMB/RPC services.
* [ ] Perform vulnerability assessment.
* [ ] Practice controlled Metasploit exploitation.
* [ ] Configure and test ADB communication with Android-x86.
* [ ] Capture traffic using Wireshark.
* [ ] Analyze suspicious network traffic.
* [ ] Deploy a basic SIEM/log-monitoring environment.
* [ ] Document vulnerabilities and remediation techniques.
* [ ] Create attack-and-defense scenarios.
* [ ] Create a final penetration-testing report.

---

# 🧠 Key Learning Outcomes

Through this project, I gained practical experience with:

* VMware virtualization
* NAT networking
* IPv4 addressing
* Static IP configuration
* Linux network administration
* Windows network configuration
* Android-x86 deployment
* ICMP and firewall behavior
* Network troubleshooting
* Network reconnaissance
* Port scanning
* Service enumeration
* Packet analysis
* Vulnerability assessment
* Cybersecurity lab design

---

# ⚠️ Ethical & Legal Disclaimer

This laboratory is designed for **educational, research, and authorized security-testing purposes**.

All penetration-testing activities should be performed only against:

* Systems owned by the lab operator
* Intentionally vulnerable laboratory machines
* Systems for which explicit authorization has been provided

Do **not** use the techniques demonstrated in this repository against public systems, organizations, networks, applications, or devices without permission.

The purpose of this project is to develop practical cybersecurity skills in a controlled environment.

---

# 👨‍💻 Project Author

**Mallikarjun Navali**

Engineering Student | Networking & Cybersecurity Learner

### Areas of Interest

* 🌐 Computer Networking
* 🔐 Cybersecurity
* 🛡️ SOC / Blue Team
* 🔎 Vulnerability Assessment
* 🐉 Kali Linux
* 📡 Network Security
* 🧪 Penetration Testing

---

## ⭐ Project Status

**🟢 Active Development**

This repository will be continuously updated as new security-testing labs, network experiments, screenshots, findings, and documentation are added.

---

> **"Learn. Build. Test. Analyze. Secure."**
