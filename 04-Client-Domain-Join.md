# Phase 4: Client Integration & Domain Join

## 🧠 The "Why" (Deep Dive)
How does a standalone Windows 10 PC know that `john.doe` is a valid user? It has to ask the Domain Controller!
Before joining a domain, the client **MUST** have the Domain Controller's IP set as its **Primary DNS**. 
*Why DNS?* Because when you type `lab.local`, the client asks the DNS server: "Where is the Domain Controller?" Once DNS replies with the DC's IP, the client uses the **Kerberos protocol** to securely authenticate the user with the DC. Without proper DNS, the domain join will fail instantly.

## 🛠️ Implementation Steps (Detailed Walkthrough)

1.  **Configuring DNS on the Client (Crucial Step):**
    *   Booted up the Windows 10 VM and logged in with the local administrator account.
    *   Opened Network Connections (`ncpa.cpl`) > Right-clicked the Ethernet adapter > **Properties**.
    *   Selected **Internet Protocol Version 4 (TCP/IPv4)** > Properties.
    *   Changed the **Preferred DNS server** to the Domain Controller's static IP: **`192.168.233.132`**.
    *   *Why?* We are telling the Windows 10 machine to ask our `DC01` server for all name resolutions.

2.  **Verifying Connectivity:**
    *   Opened Command Prompt on Windows 10 and ran `ping lab.local`. 
    *   Received successful replies, confirming the client can reach the Domain Controller.

3.  **Joining the Domain:**
    *   Opened the Run dialog (`Windows + R`) and typed **`sysdm.cpl`** to open System Properties.
    *   Navigated to the **Computer Name** tab > Clicked **Change**.
    *   Under "Member of", selected **Domain** and typed **`lab.local`**.
    *   A credential prompt appeared. Entered the Domain Admin credentials: **`LAB\Administrator`** and the server password.
    *   Received a welcome message: *"Welcome to the lab.local domain."*
    *   Restarted the Windows 10 VM to apply the changes.

4.  **Testing Centralized Authentication (The Magic Moment):**
    *   At the Windows 10 login screen, clicked on **"Other user"** (bottom left).
    *   **Username:** Entered `LAB\john.doe` (or `john.doe@lab.local`).
    *   **Password:** Entered the domain password set in Phase 3 (`Password@123`).
    *   *Result:* Windows successfully authenticated the credentials against the Domain Controller, creating a new domain profile and logging the user in.

## 🔍 Verification
*   Opened Command Prompt as the domain user and ran the **`whoami`** command.
*   The output returned **`lab\john.doe`**, proving that the user is now authenticated by the domain, not the local computer.
*   Opened `gpresult /r` to check if the client is receiving policies from the server (we will test this in Phase 5).

*(📸 Screenshots to add: DNS settings on Win10, successful ping to lab.local, Domain Join welcome popup, Login screen showing "Other user", `whoami` command output)*
