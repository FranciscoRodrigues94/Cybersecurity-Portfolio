# Project 01 – Virtual Machine & Webserver Setup

## Overview
In this project, I set up a virtualized environment using VirtualBox and Ubuntu to host a simple web server.  
The goal was to learn the basics of virtualization, system installation, networking, service configuration, and using Linux commands. 
This was my first practical lab for building cybersecurity skills after the theoretical introduction to such domains throughout my Google Cybersecurity Course.

---

## Objectives
- Install and configure a Linux virtual machine (Ubuntu).
- Set up a working web server (Apache2).
- Enable access to the web server from the host machine’s browser.
- Troubleshoot networking and firewall issues.

---

## Steps

   ### Phase 1 - Preparation of the environment – VM & OS Installation


#### Steps

1. **Download VirtualBox**
   - Downloaded VirtualBox version **7.2.2** from the official website.
   - Selected the **Windows package** for installation.

2. **Download Ubuntu ISO**
   - Downloaded **Ubuntu 24.04.3 LTS** ISO file from the official Ubuntu website.

3. **Install VirtualBox**
   - Installed VirtualBox on my local hard drive.

4. **Create New Virtual Machine**
   - Named the VM **“Ubuntu-Portfolio”**.
   - Selected Ubuntu as the guest OS.

![Create VM](./Screenshots/4_Screenshot_VM_Settings_1.jpg)

5. **Configure Virtual Hardware**
   - Set **Base Memory** to **4096 MB**.
   - Allocated **3 CPUs**.
   - *Note:* This configuration balances performance and stability:
     - 4 GB RAM is enough for Ubuntu desktop while leaving resources for the host.
     - 3 CPUs gives the VM responsiveness without overloading the host.

![Config Virtual Hardware](./Screenshots/6_Screenshot_VM_Settings_3.jpg)

6. **Create Virtual Hard Disk**
   - Created a new virtual disk of **30 GB** in VDI format.

![Create Virtual Hard Disk](./Screenshots/7_Screenshot_VM_Settings_4.jpg)


7. **Start Installation & User Setup**
   - Booted the VM with the Ubuntu ISO.
   - Followed installation steps:
     - Language, region, disk setup.
     - Created a **username and password** for login.

8. **Successful Boot**
   - The VM started successfully with Ubuntu 24.04.3 LTS installed.
   - Logged in with the created user account.
   - 
![Successful Boot](./Screenshots/8_Installed_VM_5.jpg)

Note: All screenshots of this process can be found [here](./Screenshots).

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
