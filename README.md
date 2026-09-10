# 🔐 Cybersecurity & Penetration Testing Lab Environment Setup

Building an isolated virtual lab for multi-target penetration testing, ethical hacking practice, and security research.

---

## 📌 Project Overview

This project focuses on building a dedicated, multi-OS penetration testing laboratory using **VMware Workstation**. The primary goal is to establish an isolated `10.0.0.0/24` network environment containing an attack platform (**Kali Linux**) interconnected with multiple target machines spanning **Windows** (Win 7, Win 10, Win 11) and **Android** environments. 

The lab is configured on a custom isolated virtual NAT network (`VMnet8`), enabling controlled vulnerability assessments, service enumeration, exploitation, and post-exploitation testing without exposing local physical networks or unauthorized systems to risk.

---

## 🎯 Objectives

* Configure custom virtual networking (`VMnet8` NAT) in VMware Workstation.
* Deploy and configure **Kali Linux** as the primary attack platform on `10.0.0.2`.
* Provision and network multiple target operating systems across specific IP allocations:
  * **Android-x86 Target:** `10.0.0.9`
  * **Windows 10 Target:** `10.0.0.10`
  * **Windows 11 Target:** `10.0.0.16`
  * **Windows 7 Target:** `10.0.0.7`
* Establish and verify full local network inter-VM routing and internet access (`8.8.8.8`).
* Configure custom host firewalls (ICMP ingress rules) and static IP parameters on targets.
* Establish baseline VM state recovery mechanisms.

---

## 🛡️ Purpose of the Lab

This lab provides a safe, repeatable, and completely contained ecosystem for authorized hands-on security training. Activities designed for this environment include:

* **Network Reconnaissance & Port Scanning:** Service identification across Windows and Android platforms.
* **Android Security Auditing:** ADB (Android Debug Bridge) exploitation, application assessment, and shell access.
* **Windows Exploitation Practice:** SMB, RPC, and OS-specific vulnerability assessments.
* **Packet Analysis & Traffic Inspection:** Capturing virtual interface traffic using Wireshark.
* **Exploitation & Payload Testing:** Metasploit Framework and custom exploit payload delivery.

> **⚠️ Disclaimer:** This environment and its associated documentation are intended strictly for educational and authorized security testing purposes. All testing must be confined to systems owned or explicitly authorized by the lab operator.

---

## 🏗️ Lab Architecture

```text
                        ┌────────────────────────┐
                        │   VMware Host Gateway  │
                        │       10.0.0.1         │
                        └───────────┬────────────┘
                                    │
               ┌────────────────────┴────────────────────┐
               │    VMnet8 Isolated NAT Network          │
               │           10.0.0.0/24                   │
               └─┬─────────────┬─────────────┬─────────┬─┘
                 │             │             │         │
                 ▼             ▼             ▼         ▼
          ┌─────────────┐ ┌───────────┐ ┌───────────┐ ┌───────────┐
          │  Kali Linux │ │ Android-  │ │ Windows   │ │ Windows   │
          │   (Attacker)│ │    x86    │ │ 10 / 11   │ │     7     │
          │  10.0.0.2   │ │ 10.0.0.9  │ │ .10 / .16 │ │ 10.0.0.7  │
          └─────────────┘ └───────────┘ └───────────┘ └───────────┘
