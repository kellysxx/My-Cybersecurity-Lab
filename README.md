# 🛡️ Kali Linux Cybersecurity Lab

A beginner-friendly virtual lab documenting my Kali Linux network setup, troubleshooting, and verification in Oracle VirtualBox.

![Kali Linux](https://img.shields.io/badge/Kali_Linux-2025.3-557C94?style=flat-square&logo=kalilinux&logoColor=white) ![VirtualBox](https://img.shields.io/badge/Oracle_VirtualBox-7.2-183A61?style=flat-square&logo=virtualbox&logoColor=white) ![Lab Network](https://img.shields.io/badge/Lab_Network-10.0.0.0%2F24-238F89?style=flat-square) ![NetworkWalks](https://img.shields.io/badge/NetworkWalks-Week_01-404040?style=flat-square)

## 🎯 Project overview
This project documents how I set up and verified a Kali Linux VM in Oracle VirtualBox, including its NAT Network, static IPv4 configuration, troubleshooting, and test evidence.

## 🎯 Purpose of the lab
I created this lab to practice Linux networking and cybersecurity fundamentals in a controlled environment. I will only test systems I own or have permission to assess.

## 🏗️ Lab architecture
**Windows host** → **Oracle VirtualBox** → **NAT Network** (`10.0.0.0/24`) → **Kali Linux VM** (`10.0.0.2/24`)

The Kali VM uses gateway `10.0.0.1`. The VirtualBox NAT Network is named `NatNetwork` and has DHCP enabled; Kali was later configured with a static address.

## ⚙️ Lab configuration
| Component | Configuration |
|---|---|
| Host | Windows 11 |
| Hypervisor | Oracle VirtualBox 7.2 |
| VM | Kali Linux 2025.3, 2048 MB RAM |
| Network | NAT Network, `NatNetwork`, `10.0.0.0/24` |
| Kali IPv4 | Static `10.0.0.2/24` |
| Gateway | `10.0.0.1` |
| DNS | `8.8.8.8`, `1.1.1.1` |
| Snapshot | `Static IP Verified` |

## 🪜 Setup evidence

### VirtualBox and Kali VM
![VirtualBox Manager](screenshots/virtualbox-manager.png)
![Virtual machine overview](screenshots/virtual-machine-overview.png)
![Virtual machine system settings](screenshots/virtual-machine-system-settings.png)

### NAT Network and adapter
![NAT Network settings](screenshots/nat-network-dhcp-settings.png)

The saved adapter screenshot shows Promiscuous Mode set to **Allow All** at that time; it does not confirm the current setting.
![Kali adapter settings](screenshots/kali-audio-and-network-settings.png)

### Static IPv4 and snapshot
![Kali manual IPv4 settings](screenshots/kali-ipv4-manual-settings.png)
![Kali snapshot](screenshots/kali-snapshot-Static-IP-Verified.png)

## ✅ Verification
The terminal screenshot shows `10.0.0.2/24`, the default route via `10.0.0.1`, and four successful pings to `8.8.8.8` with no packet loss. I also confirmed that `google.com` resolved. Before the static setup, Kali received `10.0.0.3/24` via DHCP.

![Static IP and connectivity verification](screenshots/kali-static-ip-verification.png)
![DHCP address before static configuration](screenshots/kali-dhcp-before-static.png)
![Connectivity and DNS verification](screenshots/dns-connectivity.png)

Commands used:
```bash
ip -4 addr
ip route
ping -c 4 8.8.8.8
getent hosts google.com
```

## 🐞 Problems I faced and how I solved them

### Connection name capitalization
I first ran `nmcli connection up "wired connection 1"` and saw `Error: unknown connection`. The saved profile was `Wired connection 1` with a capital **W**. Using the exact profile name allowed NetworkManager to activate it.

### Invalid or failed manual IPv4 settings
The IPv4 editor said Manual mode needed an address or route and that the netmask was invalid. A later attempt failed with “IP configuration could not be reserved.” My screenshots also show that I had put the gateway in the DNS field. I corrected the fields so the gateway was `10.0.0.1` and DNS contained only DNS servers.

To restore access while troubleshooting, I returned the profile to DHCP and cleared the manual values. Kali received `10.0.0.3/24`; I confirmed connectivity and name resolution, then configured `10.0.0.2/24` with gateway `10.0.0.1` and DNS `8.8.8.8` and `1.1.1.1`. I verified the result with `ip -4 addr`, `ip route`, `ping -c 4 8.8.8.8`, and `getent hosts google.com`.

## 🧠 What I learned
- How a VirtualBox NAT Network provides a private network for lab VMs.
- How to configure and verify a static IPv4 address, gateway, and DNS in Kali.
- How to troubleshoot NetworkManager connection profiles.
- Why snapshots and clear documentation are useful.

## 🧰 Tools and resources
- [Oracle VirtualBox](https://virtualbox.org/wiki/Downloads)
- [Kali Linux](https://kali.org/get-kali)

## 🔐 Safe use
This lab is for learning and authorized testing only. I will test only systems I own or have explicit permission to assess.

## 👤 Author
**Kelechi Happiness Uzoma** · Cybersecurity Intern at NetworkWalks

## 📋 Project information
| Item | Details |
|---|---|
| Program | Cybersecurity at NetworkWalks |
| Week | 01 |
| Project | Cybersecurity & Pentesting Lab Setup |
| Repository | [My-Cybersecurity-Lab](https://github.com/kellysxx/My-Cybersecurity-Lab) |

## 🙏 Credits
This Week 01 project was completed as part of Cybersecurity at NetworkWalks. The lab configuration, screenshots, and test results are my own. Software download links are listed above.
