<div align="center">

# 🔐 Cybersecurity Lab Environment Setup

**🛡️ Wireshark SOC Analyst – Network Traffic Analysis Labs**
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub Profile-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
    <img src="https://img.shields.io/badge/WireShark-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
</p>

---

## 📌 Project Overview
This project documents my hands-on experience with Wireshark through practical SOC (Security Operations Center) laboratory exercises.

The labs focus on network traffic analysis, TCP stream investigation, identifying suspicious network activity, detecting brute-force attempts, analyzing HTTP traffic, and investigating VoIP communications.

Through these exercises, I developed practical skills in examining network packets, identifying communication patterns, and understanding potential security threats.


---


## 🎯 Objectives

The main objectives of this project are to:
Understand network traffic and packet analysis.

Identify attacker and target IP addresses.

Analyze TCP connections and follow TCP streams.

Investigate HTTP communication and plaintext credentials.

Detect brute-force login attempts.

Analyze VoIP call setup and communication.

Identify suspicious network activities.

Develop practical SOC analyst investigation skills.

---

## 🛡️ Purpose of the Lab

The purpose of this lab is to develop practical skills in network traffic analysis and cybersecurity investigation using Wireshark.

Through these hands-on exercises, the objective is to understand how network communication works, analyze captured packets, identify suspicious activities, and investigate potential cyberattacks.

The lab focuses on:

Identifying attacker and target IP addresses.

Analyzing TCP connections and following TCP streams.

Investigating network communication and hidden information.

Understanding the security risks of plaintext HTTP credentials.

Detecting brute-force login attempts and suspicious authentication activities.

Analyzing VoIP communication using SIP and RTP protocols.

Developing fundamental SOC Analyst and network forensic investigation skills.

---

## 🏗️ Lab Architecture

![](https://github.com/nuzhatakbar009-debug/NETWORKWALKS-B084-WK-1PMX-WIRESHARK-SOC-ANALYST-LABS/commit/f10ce128508045e94771344d6b3ad84270cb3437#diff-1cce0f17503a38b5638c2ca0babe75726552556fc119c2f9796a919d2933a4e1)
Lab 03 – Identify the Attacker's IP

Objective: Identify the attacker's IP address by analyzing captured network traffic.

Tasks:

Capture network traffic.

Filter SYN packets.

Identify the attacker.

Identify the target.

Investigate source ports.

Identify probed and open ports.

Analyze closed-port responses.

Determine the attack type.

Result: 100/100 Marks




---

# 🪜 Lab Setup Procedure

## Step 1. Install 7-Zip

7-Zip was installed to extract the Kali Linux virtual-machine package, which may be distributed as a `.7z` archive.

**Tool:** 7-Zip

---

## Step 2. Install VirtualBox

VirtualBox was installed as the hypervisor.

---

## Step 3. Create the NAT Network

A dedicated NAT Network was created in VirtualBox.

Configuration:
Network Name: NatNetwork
IPv4 Prefix:  10.0.0.0/24
DHCP:         Enabled
IPv6:         Disabled

![](https://github.com/nuzhatakbar009-debug/NETWORKWALKS-B084-WK-1PM-1CYBERSECURITY-LAB-SETUP/blob/main/2nd%20screenshot%20-network%20setting.PNG)

A **NAT Network** was selected because multiple virtual machines connected to the same NAT Network can communicate with one another while also having outbound network connectivity.

This will allow future attacker and target VMs to communicate within the lab.


---

## Step 4. Import Kali Linux

The Kali Linux virtual machine was downloaded from the official Kali Linux website and imported into VirtualBox.

The VM network adapter was configured as follows:

```text
Adapter 1
Attached to: NAT Network
Network:     NatNetwork
Adapter Type: Intel PRO/1000 MT Desktop
```

The VM was allocated:

```text
RAM: 2048 MB
```
![](https://github.com/nuzhatakbar009-debug/NETWORKWALKS-B084-WK-1PM-1CYBERSECURITY-LAB-SETUP/blob/main/3rd%20screenshot-kali-linux.PNG)
A shared folder was also configured for transferring required files between the host operating system and the Kali VM.



---

## Step 5. Configure the Kali Linux Network

The Kali Linux network configuration was checked and configured with a consistent IPv4 address.

Example configuration:

```text
IP Address: 10.0.0.2
Subnet Mask: 255.255.255.0
Gateway: 10.0.0.1
DNS: 8.8.8.8
```

A consistent IP address makes it easier to document the lab and reference the Kali machine in future exercises.

![](https://github.com/nuzhatakbar009-debug/NETWORKWALKS-B084-WK-1PM-1CYBERSECURITY-LAB-SETUP/blob/main/4th%20%20screenshot-kali-network-setting.PNG)

---

🔎## Step 6. Create a Clean VM Snapshot

After completing the initial configuration, a VirtualBox snapshot was created.

Example snapshot name:

```text
Clean Kali - Network Setup
```

The snapshot represents the clean baseline of the laboratory.

If a future exercise changes or damages the VM configuration, the machine can be restored to this baseline.


---

# 🔎 Lab Verification

| ✅ Test                        | 🧾 Command                      | 🎯 Expected Result              |
| ----------------------------- | ------------------------------- | ------------------------------- |
| 🌐 Check IP address           | `ip a`                          | Correct Kali IP displayed       |
| 📡 Test gateway               | `ping 10.0.0.1`                 | Successful replies              |
| 🌍 Test Internet connectivity | `ping 8.8.8.8`                  | Successful replies              |
| 🔎 Test DNS resolution        | `nslookup networkwalks.com`     | Domain resolves                 |
| 🧰 Verify Nmap                | `nmap --version`                | Nmap version displayed          |
| 🔄 Verify snapshot            | Restore snapshot and run `ip a` | Baseline configuration restored |

### Example Results

```text
IP Address:
10.0.0.2/24

Gateway:
10.0.0.1

DNS:
8.8.8.8
```

---

# 🐞 Problems Encountered & Solutions

Documenting problems is an important part of the project.

## Problem 1. Internet Connectivity After Static IP Configuration

After manually configuring the IPv4 settings, Internet connectivity may fail depending on the Kali/NetworkManager configuration.

One workaround used during this lab was:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

The network connection was then restarted/rebooted and connectivity was tested again.

> **Important:** Network interface and connection names may differ between systems. Students should first identify their actual connection name before running an `nmcli` command.

---

## Problem 2. VirtualBox VT-x / Virtualization Error

The VM initially failed to start because hardware virtualization was disabled in the system firmware/BIOS.

The issue was resolved by:

1. Restarting the computer.
2. Entering BIOS/UEFI settings.
3. Enabling Intel VT-x / hardware virtualization.
4. Saving the configuration.
5. Restarting the computer.
6. Starting the Kali VM again.

After enabling virtualization, the VM started successfully.


---

# 💡 What I Learned

Through this project, I learned how to create and configure a virtual environment for cybersecurity practice.

The most important concepts I learned include:

### 1. NAT vs NAT Network

A standard NAT configuration and a NAT Network serve different purposes.

A NAT Network allows multiple VMs connected to the same virtual network to communicate with one another while providing network address translation for external connectivity.

This makes it useful for building a multi-machine cybersecurity laboratory.

### 2. Virtual Machine Networking

I learned how VirtualBox virtual network adapters connect virtual machines to different types of networks and how network configuration affects communication between machines.

### 3. Static IP Configuration

I learned how to configure and verify IPv4 addressing, subnet masks, gateways, and DNS settings in Kali Linux.

### 4. VM Snapshots

I learned that a clean snapshot should be created **before performing risky or experimental activities**.

This provides a known-good recovery point for future cybersecurity exercises.

### 5. Documentation

I learned that documenting commands, configuration, screenshots, problems, and solutions is an important part of a professional cybersecurity project.

---

# 🔐 Security & Ethical Use

This laboratory is intended strictly for education purposes only.

---

# 🔗 Tools & Resources

- **7-Zip:** [https://7-zip.org/download.html](https://7-zip.org/download.html)
- **VirtualBox:** [https://virtualbox.org/wiki/Downloads](https://virtualbox.org/wiki/Downloads)
- **Kali Linux:** [https://kali.org/get-kali](https://kali.org/get-kali)

---

# 👤 Author

**Nuzhat Shaheen**\
Cybersecurity intern (Batch: B084)

LinkedIn: [https://www.linkedin.com/in/nuzhat-akbar-a17963289)

---

## 📌 Project Information
Program Name: Cybersecurity internship  at Networkwalks|Week:01|Project 1: Lab Setup Virtualbox & KaliLinux
| 🌍 DNS Server | 8.8.8.8 | | 🔮 Future VM Range | 10.0.0.3–10.0.0.99 |
