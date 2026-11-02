# Phase 2: Deploying the Domain Controller (DC)

## 🧠 The "Why" (Deep Dive)
A **Domain Controller (DC)** is the heart of a Windows domain. It runs **Active Directory Domain Services (AD DS)**, which is essentially a highly secure database containing all users, computers, and their permissions. 
When you promote a server to a DC, you create a **Forest** (the top-level security boundary) and a **Domain** (the logical grouping of objects). 
Without a Domain Controller, every computer would have to be managed locally (Workgroup). With a DC, we achieve **Centralized Identity Management**—meaning one single login can authenticate across thousands of computers.

## 🛠️ Implementation Steps (Detailed Walkthrough)

1.  **Installing the AD DS Role:**
    *   Opened **Server Manager** on `DC01` > Clicked on **"Add roles and features"**.
    *   Installation Type: Selected **"Role-based or feature-based installation"**.
    *   Server Selection: Selected the local server (`DC01`) from the server pool.
    *   Server Roles: Checked the box for **"Active Directory Domain Services"**.
    *   *Note:* A popup appeared asking to add required features; clicked **"Add Features"** and proceeded with the default Next options until the Installation started.

2.  **Promoting the Server to a Domain Controller:**
    *   After the AD DS role installation completed, a yellow notification flag appeared in Server Manager.
    *   Clicked on the flag and selected **"Promote this server to a domain controller"**.

3.  **Deployment Configuration (Creating the Forest):**
    *   Since this is the very first server in our network, I selected **"Add a new forest"**.
    *   **Root Domain Name:** Entered **`lab.local`**. 
    *   *Why `.local`?* Using `.local` simulates an internal corporate network rather than a public internet domain.

4.  **Domain Controller Options & Passwords (Crucial Step):**
    *   **Functional Levels:** Left the Forest and Domain functional levels at `Windows Server 2016` (the default for Server 2022) to ensure compatibility.
    *   **Capabilities:** Ensured that **DNS Server** and **Global Catalog (GC)** were checked. (A DC must be a DNS server for the network to resolve domain names).
    *   **DSRM Password:** This is the most critical part. I set a strong, complex password (e.g., `Admin@123`).
    *   *Why DSRM?* Directory Services Restore Mode is a special boot mode. If Active Directory fails or gets corrupted, this password is the ONLY way to log in and restore the system offline.

5.  **DNS Options (Handling Warnings):**
    *   A yellow warning appeared: *"A delegation for this DNS server cannot be created..."* 
    *   *Action:* I safely **ignored** this warning and left the "Create DNS delegation" box unchecked. (This is normal in isolated lab environments).

6.  **Additional Options & Paths:**
    *   Verified the **NetBIOS domain name** (automatically set to `LAB`).
    *   Left the Database, Log files, and SYSVOL folders at their default paths (`C:\Windows\...`).

7.  **Prerequisites Check & Installation:**
    *   The wizard ran a prerequisite check. It showed green ticks: *"All prerequisite checks passed successfully."*
    *   Clicked **Install**. The server automatically configured the AD database and rebooted.

## 🔍 Post-Installation Verification
*   After the reboot, the login screen displayed the domain context: **`LAB\Administrator`**.
*   Logged in with the Administrator password set during OS installation.
*   Opened **Server Manager** and confirmed that **AD DS** and **DNS** roles were successfully running with a green health status.

*(📸 Screenshots to add: AD DS installation progress, Forest creation screen, DSRM password setup, DNS Warning screen, Prerequisites Passed Screen, Login Screen with LAB\Administrator)*
