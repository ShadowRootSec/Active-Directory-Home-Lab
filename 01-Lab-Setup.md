# Phase 1: Virtual Environment & Server Provisioning

## 🧠 The "Why" (Deep Dive)
Before building a network, we need a safe, isolated environment. Using a **Hypervisor (VMware)** allows us to simulate physical servers on our local machine. 
We chose **Windows Server 2022 (Datacenter - Desktop Experience)** because:
*   **Desktop Experience:** Gives us a GUI (Graphical User Interface), which is essential for beginners to visualize AD.
*   **Datacenter Edition:** It’s the highest tier, supporting all advanced features we might test later (like nested virtualization).

## 📥 Prerequisites & Official Downloads
To replicate this lab, you will need the following software. Please download them only from their official sources:

*   **Hypervisor:** [VMware Workstation Pro](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware%20Workstation%20Pro)
*   **Server OS:** [Windows Server 2022 Evaluation ISO (Microsoft Official)](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022)
*   **Client OS:** [Windows 10 Enterprise Evaluation (Microsoft Official)](https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise)

## 🛠️ Implementation Steps (Detailed Walkthrough)

1.  **VM Provisioning & Hardware Allocation:**
    *   Opened VMware Workstation and created a **Custom (Advanced)** Virtual Machine.
    *   **Memory:** Allocated **4 GB (4096 MB)** RAM to ensure smooth performance of the Windows Server GUI.
    *   **Disk:** Provisioned a **100 GB** virtual disk. 
    *   *Pro-Tip:* Selected **"Split virtual disk into multiple files"** and left **"Allocate all disk space now"** unchecked. This creates a "Thin Provisioned" disk, meaning it will only take up actual space on my host PC as data is written, saving local storage.

2.  **OS Installation & Bypassing the VMware Bug:**
    *   **The Bug:** When selecting the Windows Server 2022 ISO in VMware's "Easy Install" mode, it threw an error: *"Windows cannot find the Microsoft Software License Terms."*
    *   **The Fix:** Cancelled the wizard and created the VM using **"I will install the operating system later"** to bypass Easy Install. Manually attached the ISO via VM Settings.
    *   At the boot screen, promptly pressed a key to *"Press any key to boot from CD or DVD"*.
    *   **OS Selection:** Chose **Windows Server 2022 Datacenter Evaluation (Desktop Experience)**. 
    *   *Why Desktop Experience?* It installs the Graphical User Interface (GUI), which is essential for visualizing AD tools, unlike the Server Core (command-line only) version.
    *   Selected **Custom Installation** and installed the OS on the 100GB unallocated space.

3.  **Baseline Configuration (Post-Installation):**
    *   **Administrator Password:** Set a complex password (e.g., `Admin@123`) as Windows enforces password complexity by default.
    *   **Installing VMware Tools:** Went to `VM > Install VMware Tools`. Opened the virtual CD drive, ran `setup64.exe`, and rebooted. 
    *   *Why?* This enables seamless mouse integration, full-screen resolution, and host-to-guest clipboard sharing.
    *   **Renaming the Server:** Opened Server Manager > Local Server > Changed the random computer name (e.g., WIN-XXXXX) to **`DC01`** and restarted.
    *   **Static IP Assignment:** 
        *   Navigated to Network Adapter Settings > IPv4 Properties.
        *   Set IP: **`192.168.233.132`**, Subnet: `255.255.255.0`, Gateway: `192.168.233.2` (VMware NAT default).
        *   Set Preferred DNS: **`127.0.0.1`** (Loopback).
        *   *Why Static IP?* A Domain Controller acts as the DNS server for the network. If its IP changes dynamically, all domain clients will lose connection to the server.

*(📸 Screenshots to add: VMware Disk Allocation screen, OS Selection menu (Datacenter Desktop Experience), Static IP Configuration window)*
