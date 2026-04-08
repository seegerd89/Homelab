# 🏠 Homelab Setup – D Seeger

## 📖 Overview
This project documents my personal homelab environment used for learning and practicing system administration, networking, and containerized services.

The setup focuses on self-hosting, network services, and secure remote access.

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
- Raspberry Pi 4 (KVM over IP solution)
- Raspberry Pi 5 (Pi-hole)  
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

## 🖥️ Core Systems

| System        | Purpose                          |
|--------------|----------------------------------|
| TrueNAS      | Storage + container platform     |
| Raspberry Pi 5 | DNS filtering (Pi-hole)        |
| Raspberry Pi 4 | Remote Management (KVM)        |
| Fedora KDE   | Linux client / daily driver      |
| Windows 11   | Secondary OS (gaming/work)       |

---

## 📦 Services

### 🎬 Media & Applications (Containerized on TrueNAS)
- **Jellyfin** – Media streaming server  
- **Navidrome** – Music streaming server  
- **Minecraft Server** – Game server  

### 🌐 Network Services
- **Pi-hole** – DNS-based ad blocking and filtering  
- **Tailscale** – Secure VPN (WireGuard-based)
- **KVM over IP (Raspberry Pi 4)** - Remote hardware-level access to NAS

---

## 🌍 Network Architecture

- Pi-hole acts as the central DNS server  
- All clients use Pi-hole for DNS resolution  
- Remote access is handled via Tailscale VPN  
- Services are hosted in containers on TrueNAS  

---

## ⚙️ Setup & Responsibilities

- Installation and configuration of TrueNAS  
- Deployment and management of containerized services  
- Setup of DNS filtering using Pi-hole  
- Configuration of secure remote access via Tailscale  
- Linux system usage and administration (Fedora KDE)
- Implementation of a KVM over IP solution usinf Raspberry Pi 4 for remote system access
- Low-level troubleshooting and remote system control independent of OS/network state

---

## 🛠️ Troubleshooting 

### ❌ Issue: Minecraft lagging  
- **Cause:** Server installed on slow HDD  
- **Solution:** added 2x120GB Sata-SSD in Mirror  

--- 

### ❌ Issue: Troubleshooting  
- **Cause:** Server running headless out of reach  
- **Solution:** PiKVM on Raspberry Pi 4  

---

## 📚 Key Learnings

- Fundamentals of system administration  
- Networking concepts (DNS, VPN, routing)  
- Containerization and service isolation  
- Structured troubleshooting and problem solving  

---

## 🚀 Future Improvements

- Implement monitoring (e.g. Prometheus/Grafana)  
- Backup strategy optimization  
- High availability concepts  
- Expand automation (scripts, cron jobs)  

---

## 📌 Notes
This homelab is continuously evolving and used as a hands-on learning environment for IT skills, especially in system administration.
