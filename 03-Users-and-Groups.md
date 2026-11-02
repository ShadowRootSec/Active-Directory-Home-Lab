# Phase 3: Organizational Structure, Users & Security Groups

## 🧠 The "Why" (Deep Dive)
In a real enterprise environment, dumping all users into a single folder creates a massive administrative headache. To mirror a real company, we use **Organizational Units (OUs)**. OUs act like folders that represent departments (IT, HR, Sales). This structure is crucial because Group Policies (GPOs) are applied at the OU level. 

Furthermore, we never assign permissions directly to individual users. Instead, we use **Security Groups** (a concept called **RBAC - Role-Based Access Control**). If an employee changes departments, you don't have to change 50 file permissions; you simply move their user account from one group to another.

## 🛠️ Implementation Steps (Detailed Walkthrough)

1.  **Opening the Management Console:**
    *   On the Domain Controller (`DC01`), opened Server Manager > **Tools** > **Active Directory Users and Computers (ADUC)**.
    *   *Pro-Tip:* You can also open the Run dialog (`Windows + R`) and type `dsa.msc` to launch it instantly.

2.  **Creating Organizational Units (OUs):**
    *   In ADUC, right-clicked on the root domain **`lab.local`** > Selected **New** > **Organizational Unit**.
    *   Named the parent OU: **`THM`** (simulating a company name).
    *   Right-clicked on the `THM` OU > Created a child OU named **`IT`**.
    *   *Why?* This ensures that any IT-specific rules will only apply to people inside this folder.

3.  **Creating a New User Account:**
    *   Right-clicked on the `IT` OU > Selected **New** > **User**.
    *   **First name:** `John`, **Last name:** `Doe`.
    *   **User logon name:** Set to **`john.doe`** (This is the username used for login).
    *   **Password Setup:** Entered a strong, complex password (e.g., `Password@123`).
    *   *Important Config:* Unchecked **"User must change password at next logon"** to ensure smooth testing without being prompted for a password change immediately.

4.  **Creating a Security Group & Implementing RBAC:**
    *   Right-clicked on the `IT` OU > Selected **New** > **Group**.
    *   **Group name:** `IT_Admins`.
    *   **Group scope:** `Global` (Default).
    *   **Group type:** `Security` (Used for assigning permissions).
    *   **Adding User to Group:** Right-clicked `IT_Admins` > Properties > **Members** tab > Clicked **Add** > Typed `john.doe` > Checked Names > OK. 
    *   *Result:* John Doe is now part of the IT Admins group.

## 🔍 Verification & Testing
*   **Verifying the User:** Opened Command Prompt on the Domain Controller and ran `dsquery user -samid john.doe` to confirm the user was successfully created in the directory.
*   **Verifying Group Membership:** To confirm RBAC was implemented correctly, I ran the following command in Command Prompt:
    `net user john.doe /domain`
    *   This command displayed all the properties of John Doe, including the **"Local Group Memberships"** and **"Global Group memberships"** sections, where `IT_Admins` was clearly listed.
*   Also visually confirmed in ADUC that `john.doe` is inside the `IT` OU and added to the `IT_Admins` Security Group.

*(📸 Screenshots to add: ADUC Tree view (THM > IT), User creation wizard, Group creation screen, `net user` command output)*
