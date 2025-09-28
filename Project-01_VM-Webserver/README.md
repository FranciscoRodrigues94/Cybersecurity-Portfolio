# Project 01 – Virtual Machine & Webserver Setup

## Overview
In this project, I set up a virtualized environment using VirtualBox and Ubuntu to host a simple web server.  
The goal was to learn the basics of virtualization, system installation, networking, and service configuration.  
This was my first practical lab for building cybersecurity skills.

---

## Objectives
- Install and configure a Linux virtual machine (Ubuntu).
- Set up a working web server (Apache2).
- Enable access to the web server from the host machine’s browser.
- Troubleshoot networking and firewall issues.

---

## Steps

1. **Virtual Machine Setup**
   - Installed **VirtualBox** on host machine (Windows).
   - Created a new VM and installed **Ubuntu 22.04 LTS**.
   - Configured resources (RAM, disk, network adapter).

2. **System Preparation**
   - Updated the system using:
     ```bash
     sudo apt update && sudo apt upgrade -y
     ```

3. **Webserver Installation**
   - Installed Apache2:
     ```bash
     sudo apt install apache2 -y
     ```
   - Verified service status:
     ```bash
     systemctl status apache2
     ```

4. **Networking Configuration**
   - Configured VM with **host-only adapter** to allow access from host browser.
   - Verified IP address with:
     ```bash
     ip a
     ```
   - Tested access from host machine via:
     ```
     http://<VM-IP>
     ```

5. **Troubleshooting**
   - Encountered errors with port 80 and connection refused.
   - Adjusted VirtualBox network settings and confirmed Apache was listening.
   - Final test: accessed the default Apache webpage from host browser successfully.

---

## Evidence
- [ ] Screenshot: VirtualBox VM running Ubuntu  
- [ ] Screenshot: Apache service status (running)  
- [ ] Screenshot: Browser on host showing the Apache default page  

*(Add screenshots into a `/screenshots` folder and link them here.)*

---

## Key Learnings
- Basics of creating and managing virtual machines.
- Installing and configuring a web server in Linux.
- Importance of network adapter configuration (NAT vs Host-Only).
- First exposure to troubleshooting connectivity issues between host and VM.

---

## Next Steps
- Harden the server (UFW firewall, SSH keys, disable root login).
- Capture traffic with Wireshark to analyze HTTP requests.
- Document secure baseline configurations.
