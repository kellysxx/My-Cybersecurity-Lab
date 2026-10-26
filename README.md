<div align="center">

# 🛡️ My Cybersecurity Lab

**A Kali Linux lab I built and tested in VirtualBox**

 <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square\&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ver-Virtualbox%20v7.2-0070C0?style=flat-square\&labelColor=000000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square\&labelColor=000000\&logo=kalilinux\&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square\&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square\&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square\&labelColor=000000\&logo=kalilinux\&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square\&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square\&labelColor=0070C0\&logo=github\&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-404040?style=flat-square\&labelColor=C00000\&logo=kalilinux\&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square\&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square\&labelColor=000000\&logo=kalilinux\&logoColor=white" />
</p>

</div>

A hands-on learning project documenting my own virtual machine, network configuration, troubleshooting, and verification evidence.

> The repositories in Credits were references for the topic and documentation structure. The configuration, screenshots, and test results below are from my own lab.

## 📌 Lab at a glance

| Component | My setup |
|---|---|
| Host operating system | Windows |
| Hypervisor | Oracle VirtualBox |
| Virtual machine | Kali Linux 2025.3 |
| Kali memory | 2048 MB |
| Network mode | NAT Network |
| NAT Network name | `NatNetwork` |
| IPv4 network | `10.0.0.0/24` |
| NAT DHCP | Enabled on the VirtualBox network |
| Kali IPv4 configuration | Manual/static |
| Kali address | `10.0.0.2/24` |
| Gateway | `10.0.0.1` |
| DNS servers | `8.8.8.8`, `1.1.1.1` |
| Snapshot | `Static IP Verified` |

## 🪜 Setup walkthrough

### 1. VirtualBox Manager

I used VirtualBox Manager to manage the Kali virtual machine and NAT Network.

![VirtualBox Manager](screenshots/virtualbox-manager.png)

### 2. Kali virtual machine

The VM is Kali Linux 2025.3 with 2048 MB of memory.

![Virtual machine overview](screenshots/virtual-machine-overview.png)

![Virtual machine system settings](screenshots/virtual-machine-system-settings.png)

### 3. NAT Network

I created a NAT Network named `NatNetwork` with the IPv4 prefix `10.0.0.0/24`. DHCP is enabled on the VirtualBox network and IPv6 is disabled.

![NAT Network settings](screenshots/nat-network-dhcp-settings.png)

### 4. Kali network adapter

Adapter 1 connects Kali to the `NatNetwork` using the Intel PRO/1000 MT Desktop adapter. I set Promiscuous Mode to **Deny** for the current setup. The saved screenshot shows the earlier **Allow All** setting.

![Kali adapter settings](screenshots/kali-audio-and-network-settings.png)

### 5. Static IPv4 settings

I configured `Wired connection 1` with address `10.0.0.2/24`, gateway `10.0.0.1`, and DNS.

![Kali manual IPv4 settings](screenshots/kali-ipv4-manual-settings.png)

### 6. Snapshot

After verifying the network configuration, I saved a VirtualBox snapshot named `Static IP Verified`.

![Kali snapshot](screenshots/kali-snapshot-Static-IP-Verified.png)

## ✅ Verification

The terminal evidence shows Kali using the static address `10.0.0.2/24`, with a default route through `10.0.0.1`. Four pings to `8.8.8.8` succeeded with 0% packet loss.

![Kali static IP and connectivity verification](screenshots/kali-static-ip-verification.png)

Earlier in the setup, Kali received `10.0.0.3/24` dynamically. This screenshot records the DHCP state before I configured the static address.

![Kali DHCP address before static configuration](screenshots/kali-dhcp-before-static.png)

I also checked that `google.com` resolves and that the VM can reach `8.8.8.8`.

![Kali connectivity and DNS verification](screenshots/dns-connectivity.png)

## 🧰 Commands used

```bash
ip -4 addr
ip route
ping -c 4 8.8.8.8
getent hosts google.com
```

## 🔧 Troubleshooting note

I initially ran into validation errors while entering the manual IPv4 settings. I corrected the connection configuration and then verified the address, route, ping, and DNS resolution from Kali.

## 🔐 Safe use

This lab is for learning and authorized testing. I will only test systems I own or have explicit permission to assess.


This repository documents my own VM configuration, screenshots, and results.
