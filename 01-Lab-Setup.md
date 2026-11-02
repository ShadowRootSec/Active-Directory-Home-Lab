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

## 🛠️ Implementation Steps
1.  **VM Provisioning:** Created a VM with 4GB RAM and a 100GB disk. 
    *   *Pro-Tip:* We used **"Dynamically Expanding Disk"** (Split into multiple files) so it only takes up actual storage on the host, not the full 100GB upfront.
2.  **OS Installation:** Encountered the infamous VMware "Easy Install" license bug. 
    *   *Fix:* Bypassed it by selecting "I will install the OS later," manually attaching the ISO, and selecting `Datacenter Evaluation (Desktop Experience)`.
3.  **Baseline Config:** 
    *   Installed **VMware Tools** for seamless clipboard sharing and better display resolution.
    *   Renamed the PC to **`DC01`** (Standard naming convention for a Domain Controller).
    *   Assigned a **Static IP** (`192.168.233.132`) and set DNS to `127.0.0.1`. 
    *   *Why Static IP?* Because a Domain Controller is the DNS server for the network. If its IP changes, the whole network breaks!

*(📸 Screenshots to add: VM Settings, OS Selection menu, Static IP configuration)*
