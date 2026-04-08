# 🏠 Homelab Setup – Daniel Seeger

## 📖 Overview
This project documents my personal homelab environment used for learning and practicing system administration, networking, and containerized services.

The setup focuses on self-hosting, network services, and secure remote access.

---

## 🧰 Hardware

- NAS System running TrueNAS Community 25.04
- Raspberry Pi 5 (Pi-hole)  
- Desktop PC (Fedora KDE 43 / Windows 11)

---

## 🖥️ Core Systems

| System        | Purpose                          |
|--------------|----------------------------------|
| TrueNAS      | Storage + container platform     |
| Raspberry Pi | DNS filtering (Pi-hole)          |
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

---

## 🛠️ Troubleshooting Examples

### ❌ Issue: Container not reachable
- **Cause:** Port conflict  
- **Solution:** Adjusted container port configuration  

---

### ❌ Issue: DNS resolution not working
- **Cause:** Incorrect upstream DNS configuration in Pi-hole  
- **Solution:** Fixed DNS settings and verified using `nslookup`  

---

### ❌ Issue: Remote access unavailable
- **Cause:** No external access configured  
- **Solution:** Implemented Tailscale VPN  

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
