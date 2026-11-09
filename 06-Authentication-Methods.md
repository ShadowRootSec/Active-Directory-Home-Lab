# Phase 6: Understanding Authentication Methods (Kerberos vs NTLM)

## 🧠 The "Why" (Deep Dive)
Active Directory does not just store passwords; it heavily relies on authentication protocols to verify identities. The two primary protocols in Windows environments are **Kerberos** (modern, default) and **NTLM** (legacy). Understanding these is crucial because most advanced AD attacks (like Kerberoasting and Pass-the-Hash) target these specific protocols.

## 🔑 1. Kerberos Authentication (Ticket-Based)
Kerberos uses a ticketing system to allow users to access services without re-entering passwords (Single Sign-On). 
*   **The KDC (Key Distribution Center):** Located on the Domain Controller, it handles all requests.
*   **TGT (Ticket Granting Ticket):** The user authenticates once and receives a TGT (a temporary pass).
*   **TGS (Ticket Granting Service):** Using the TGT, the user requests a specific service ticket (TGS) for the resource they want to access (e.g., a database).

**Lab Practical:** I ran the `klist` command on the Windows 10 client to view the Kerberos tickets granted to `john.doe`, confirming the presence of the TGT.

## 🛡️ 2. NTLM Authentication (Challenge-Response)
NTLM is a legacy protocol kept for backward compatibility. It uses a 3-way handshake:
1.  **Negotiate:** Client requests access.
2.  **Challenge:** Server sends a random number.
3.  **Authenticate:** Client encrypts the challenge using its password hash and sends it back to the Domain Controller for verification.

**Security Implication:** NTLM hashes are highly vulnerable to **Pass-the-Hash** attacks. Therefore, modern environments aim to disable NTLM completely.

*(📸 Screenshots to add: `klist` command output on the Windows 10 client)*
