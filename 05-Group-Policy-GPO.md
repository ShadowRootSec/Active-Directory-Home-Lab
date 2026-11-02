# Phase 5: Enforcing Security with Group Policy (GPO)

## 🧠 The "Why" (Deep Dive)
Group Policy is the ultimate system administrator tool. It allows you to control thousands of computers and users from one central console. 
A common enterprise scenario: A company wants to prevent employees from accessing the Control Panel to stop them from installing unauthorized software or changing network settings. Instead of walking to every PC, we create a **GPO**, link it to an **OU**, and let Active Directory enforce it automatically.

## 🛠️ Implementation Steps (Detailed Walkthrough)

1.  **Opening Group Policy Management:**
    *   On the Domain Controller (`DC01`), opened Server Manager > **Tools** > **Group Policy Management**.

2.  **Creating a New GPO:**
    *   Expanded the tree: `Forest: lab.local` > `Domains` > `lab.local`.
    *   Right-clicked on **Group Policy Objects** > Selected **New**.
    *   Named the GPO: **`Disable_Control_Panel`** and clicked OK.

3.  **Editing the GPO (Configuring the Restriction):**
    *   Right-clicked the newly created GPO and selected **Edit**.
    *   Navigated to the following path: 
        `User Configuration` > `Policies` > `Administrative Templates` > `Control Panel`.
    *   On the right pane, double-clicked the policy: **"Prohibit access to Control Panel and PC settings"**.
    *   Selected **Enabled** > Clicked **Apply** > **OK**.
    *   *Technical Note:* We configured this under **User Configuration** because we want to restrict the user (`john.doe`), regardless of which computer he logs into.

4.  **Linking the GPO to the Target OU:**
    *   Right-clicked the **`THM`** Organizational Unit (where our IT users reside) > Selected **Link an existing GPO**.
    *   Selected `Disable_Control_Panel` and clicked OK.
    *   *Result:* The GPO is now enforced on the THM OU.

5.  **Forcing Policy Update on the Client:**
    *   Switched to the Windows 10 Client VM and logged in as `LAB\john.doe`.
    *   Opened Command Prompt as Administrator and ran the command: **`gpupdate /force`**.
    *   After running it on the client and restarting the VM, the policy was successfully pulled from the DC.

6.  **Verifying the Restriction:**
    *   After restarting and logging back in as `john.doe`, I attempted to open the Control Panel.
    *   **Result:** A Windows security restriction popup appeared: *"This operation has been cancelled due to restrictions in effect on this computer. Please contact your system administrator."*
    *   This confirmed that centralized management was working perfectly.

## 🔍 Technical Takeaways
*   **GPO Application:** GPOs are pulled by the client machine during startup or login.
*   **Troubleshooting:** Running `gpresult /r` on the client helps verify which policies are actually applied.
*   **OU vs. Security Group:** We linked the GPO to an OU, but remember that GPOs can also be filtered using Security Groups in the "Scope" tab (under Security Filtering).

*(📸 Screenshots to add: Creating the GPO, Editing the "Prohibit access" setting, Linking GPO to OU, `gpupdate /force` output, The Restriction Error Popup on Windows 10)*
