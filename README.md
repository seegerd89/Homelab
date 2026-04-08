# 🏠 Homelab Setup – D Seeger

## Overview📖
This repository documents my personal homelab environment, used to build hands-
on experience in **system administration, networking, and self-hosted
infrastructure**.
The setup focuses on **security-first principles**, containerized services, and
secure remote access without exposing services directly to the public internet.
---

## 🧰 Hardware

- NAS System running TrueNAS Community 25.04
  - Mainboard Asus ROG Strix B350-F Gaming
  - AMD Ryzen 7 1800X
  - 64GB ECC DDR4-RAM
  - NVidia GeForce Quadro P620
  - GLOTRENDS ST7315 1-Port 10Gb SFP+
  - 8-Port PCI SATA-Card
  - 1x 1TB Nvme-SSD (OS)
  - 2x 120GB Sata-SSD (MineCraft)
  - 5x 6TB Sata-HDD (Storage)
- Raspberry Pi 4 (KVM over IP – remote hardware access)
- Raspberry Pi 5 (Pi-hole – DNS filtering)
- Desktop PC (Fedora KDE 43 / Windows 11)
  - Mainboard Asus ROG Crosshair VIII Formula
  - AMD Ryzen 7 5800X
  - 32GB DDR4-RAM
  - NVidia GeForce RTX 3070 Ti
  - 1x 1TB Nvme-SSD (Windows)
  - 1x 1TB Nvme-SSD (Fedora Kde 43)
  - 1x 2TB Sata-SSD (gaming NTFS)
  - 1x 2TB Nvme-SSD via internal USB 3.2 Gen 2 (gaming ext4)

---

## Core Systems🖥️
| System | Purpose |
|------------------|--------------------------------------|
| TrueNAS | Storage + container platform |
| Raspberry Pi 5 | DNS filtering (Pi-hole) |
| Raspberry Pi 4 | Out-of-band management (KVM) |
| Fedora KDE | Linux client / daily driver |
| Windows 11 | Secondary OS |
---
## Services📦
### Containerized Applications (TrueNAS)🎬
- **Jellyfin** – Media streaming
- **Navidrome** – Music streaming
- **Minecraft Server** – Game server
### Network & Infrastructure🌐
- **Pi-hole** – DNS-based ad blocking and filtering
- **Tailscale** – Secure VPN (WireGuard-based)
- **SSH (Key-based authentication)** – Secure remote management
---
## Security Approach🔐
- No public exposure of internal services
- Remote access exclusively via **VPN (Tailscale)**
- **SSH key-based authentication** (no password login)
- Separation of infrastructure components
- Out-of-band access via **KVM over IP**
---
## Setup & Responsibilities⚙️
- Installation and configuration of TrueNAS
- Deployment and management of containerized services
- Setup of DNS filtering with Pi-hole
- Implementation of secure remote access via Tailscale
- Configuration of SSH key-based authentication
- Implementation of KVM over IP using Raspberry Pi for low-level system access
- Linux system usage and administration (Fedora KDE)
---

## 🛠️ Troubleshooting 

### ❌ Issue: Minecraft lagging  
- **Cause:** Server installed on slow HDD  
- **Solution:** added 2x120GB Sata-SSD in Mirror  

---  

### ❌ Issue: System sometimes freezing over night  
- **Cause:** Am4 Bug with C-States  
- **Solution:** disabled all C-States  

---

### ❌ Issue: general Troubleshooting  
- **Cause:** Server running headless out of reach  
- **Solution:** PiKVM on Raspberry Pi 4  

---

## Key Learnings📚
- System administration fundamentals
- Networking concepts (DNS, VPN, routing)
- Containerization and service isolation
- Secure infrastructure design
- Structured troubleshooting and debugging
---
## Future Improvements🚀
- Monitoring (Prometheus / Grafana)
- Automated backups
- Configuration management (Ansible)
- Advanced firewalling & network segmentation
---
## Notes📌
This homelab is continuously evolving and serves as a hands-on learning
environment for real-world IT infrastructure and system administration.
