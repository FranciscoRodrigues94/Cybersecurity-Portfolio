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

## Phase 1 - Preparation of the environment – VM & OS Installation


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

## Phase 2 – Firewall Setup & SSH Access

In this phase, I secured the VM by configuring a basic firewall (UFW – Uncomplicated Firewall) and enabling SSH access.

### Steps Performed

1. **Installed UFW (Uncomplicated Firewall)**  
   - Command used:  
     ```bash
     sudo apt install ufw -y
     ```
   - UFW was already installed and updated to the newest version.  
   ![UFW Install](./Screenshots/Screenshot%20apt%20install.jpg)

2. **Enabled the Firewall**  
   - Command used:  
     ```bash
     sudo ufw enable
     ```
   - Output confirmed that UFW is active and will start automatically on system boot.  
   ![Firewall Enabled](./Screenshots/Screenshot%20Firewall%20installed.jpg)

3. **Allowed SSH Connections**  
   - First attempt:  
     ```bash
     sudo ufw allow OpenSSH
     ```
     Result: Error – no profile found for `OpenSSH`.  
   - Successful attempt:  
     ```bash
     sudo ufw allow ssh
     ```
   - This created rules for both IPv4 and IPv6.  
   ![SSH Rule](./Screenshots/Screenshot%20Firewall%20added%20ssh.jpg)

4. **Checked Firewall Status**  
   - Command used:  
     ```bash
     sudo ufw status
     ```
   - Output confirmed UFW was active and rules for SSH were applied.  
   ![Firewall Status](./Screenshots/Screenshot%20Firewall%20stauts.jpg)

Note: All screenshots of this process can be found [here](./Screenshots).

---

### Key Learnings (Phase 2 – Firewall Setup & SSH Access)

- **Firewall Basics**: Understood the role of UFW as a simple but effective firewall tool for Linux.  
- **Service Profiles vs Ports**: Learned the difference between allowing services via profile names (`OpenSSH`) vs directly allowing ports (`ssh`).  
- **Error Handling**: Encountered and resolved the “profile not found” error for OpenSSH, which reinforced the importance of knowing fallback commands.  
- **IPv6 Consideration**: UFW automatically applied rules for both IPv4 and IPv6, improving coverage.  
- **Security Practice**: Enabling UFW early in a setup is a good security habit before exposing any services externally.  

---

## Phase 3 – Networking & Port Forwarding

In this phase, I configured networking in VirtualBox to make my Apache server accessible from the host machine. This involved setting up **NAT port forwarding**, adjusting firewall rules, and validating external access.

### Steps Performed

1. **Configured NAT with Port Forwarding**  
   - Went into VM settings → Network → Adapter 1 → Attached to NAT.  
   - Enabled **Port Forwarding Rule**:  
     - Name: Apache  
     - Protocol: TCP  
     - Host Port: 8080  
     - Guest Port: 80  
   - This allows requests on `localhost:8080` on the host to be redirected to port `80` inside the VM (where Apache runs).  
   ![NAT Port Forwarding](./Screenshots/1_Screenshot%20NAT%20Configs.jpg)

2. **Checked Apache Listening Ports**  
   - Verified Apache was listening on port 80.  
   - Command used:  
     ```bash
     sudo ss -tuln | grep 80
     ```
   ![Apache Listening](./Screenshots/2_Error_Host%20doesnt%20open%20localhost_8080.jpg)

3. **Allowed Apache in UFW Firewall**  
   - Added a firewall rule to allow HTTP/HTTPS traffic:  
     ```bash
     sudo ufw allow 'Apache Full'
     ```
   - Verified the rules:  
     ```bash
     sudo ufw status verbose
     ```
   ![Firewall Rule Added](./Screenshots/3_Added%20FW%20Rule.jpg)  
   ![Firewall Status](./Screenshots/5_Check%20Allowence.jpg)

4. **Troubleshooting Connection**  
   - First tried accessing `http://localhost:8000` and got a connection refused error.  
   ![Error 8000](./Screenshots/4_Error%20Browser%20Host.jpg)

   - After correcting to `http://localhost:8080`, the Apache page successfully loaded on the host browser.  
   ![Apache OK Host](./Screenshots/6_Host%20OK.jpg)

---

### Key Learnings (Phase 3 – Networking & Port Forwarding)

- **NAT Networking in VirtualBox**: Learned that the VM uses NAT to connect to the internet, but port forwarding is required for external (host-to-guest) access.  
- **Port Forwarding**: Configured a mapping from **host port 8080 → guest port 80**, allowing the Apache service inside the VM to be reachable from the host machine browser.  
- **Apache Default Port**: Understood that Apache runs by default on port **80**, so without forwarding, the host cannot access it directly.  
- **Firewall Configuration**: Added `Apache Full` rule in UFW to allow incoming HTTP/HTTPS traffic, reinforcing the importance of securing services.  
- **Troubleshooting Mindset**: First attempt with wrong port (`8000`) failed, which highlighted the importance of verifying correct port bindings and firewall rules.  
- **Validation**: Confirmed Apache availability using both terminal (`ss -tuln`, `curl`) and browser access from the host machine.  

---
