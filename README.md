# secure-linux-headless-workstation

# Secure Linux Headless Workstation

A hardened, headless Ubuntu workstation configured for secure remote administration via xRDP and SSH, optimized for lightweight performance and infrastructure lab use.

This project documents the implementation of a monitorless Linux system designed to simulate a remote cloud node or secure administrative workstation.

---

## 🎯 Project Objectives

- Enable Ubuntu to boot without a physical monitor (headless operation)
- Resolve black screen issues caused by missing EDID display detection
- Configure secure remote access via xRDP and SSH
- Replace GNOME with lightweight XFCE for improved remote performance
- Optimize session stability and display manager configuration
- Implement baseline security controls for home-lab infrastructure

---

## 🏗 Architecture Overview

**Environment:**
- Ubuntu Desktop (22.04/24.04 compatible)
- xRDP for remote desktop access
- XFCE desktop environment
- Xorg dummy display driver
- UFW firewall
- Optional Brave private-mode launcher

**Access Model:**

Local Network → xRDP / SSH → Headless Linux Node

---

## 🔧 Key Technical Implementations

### 1️⃣ Headless Display Configuration

Ubuntu desktop environments typically fail to initialize without a connected monitor due to EDID detection.

This project resolves that issue by:

- Installing the Xorg dummy video driver
- Creating a persistent virtual display configuration
- Forcing a 1920x1080 framebuffer in `/etc/X11/xorg.conf.d/`

Result:
✔ System boots without HDMI attached  
✔ Remote sessions initialize properly  
✔ No black screen on login  

---

### 2️⃣ Desktop Environment Optimization

GNOME was replaced with XFCE to:

- Reduce CPU and memory overhead
- Improve responsiveness over RDP
- Minimize animation and rendering load
- Improve stability in headless environments

XFCE was explicitly configured as the xRDP session.

---

### 3️⃣ Remote Access Configuration

- xRDP configured to use Xorg backend
- Session startup modified for clean XFCE initialization
- SSH service enabled for administrative access
- Firewall configured to allow only required ports

---

### 4️⃣ Security Controls Implemented

- UFW firewall enabled (default deny incoming)
- Only SSH (22) and RDP (3389) allowed internally
- System updates maintained
- Remote access restricted to home network (no port forwarding)

This mirrors secure remote-access design principles used in cloud-hosted Linux nodes.

---

## 🚀 Installation Summary

### Install xRDP
```bash
sudo apt update
sudo apt install xrdp xorgxrdp -y
sudo systemctl enable --now xrdp
