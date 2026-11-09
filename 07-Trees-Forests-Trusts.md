# Phase 7: Trees, Forests & Trusts

## 🧠 The "Why" (Deep Dive)
In small environments, a single Active Directory domain is sufficient. However, in large multinational enterprises, the AD infrastructure expands into **Trees** and **Forests**. Understanding these structures is critical for managing large-scale networks and understanding cross-domain security boundaries.

## 🌳 1. Trees
A Tree is a collection of one or more domains that share a contiguous namespace. 
*   *Example:* If a company has `lab.local` and creates a European branch domain named `europe.lab.local`, both domains form a Tree.
*   *Trust:* A two-way, transitive trust is automatically established between parent and child domains in a tree.

## 🌲 2. Forests
A Forest is the top-level security boundary in Active Directory. It is a collection of one or more Trees that do not share a contiguous namespace.
*   *Example:* If `lab.local` acquires a different company with the domain `thm.com`, they form a Forest.
*   *Trust:* Forest Trusts must be manually created to allow resource sharing between separate trees.

## 🤝 3. Trusts
Trusts define the access direction between domains.
*   **One-way (Directional):** Users in Domain A can access Domain B, but not vice versa.
*   **Two-way (Bidirectional):** Both domains can access each other's resources.
*   **Transitive:** The trust extends beyond two domains. If A trusts B, and B trusts C, then A automatically trusts C.

## 🔬 Lab Practical & Verification
*   Opened **Active Directory Domains and Trusts** tool on the Domain Controller (`dc01`).
*   Right-clicked the `lab.local` domain and viewed the **Properties** > **Trusts** tab. 
*   *Result:* Since our lab consists of only a single domain, no external trusts exist. However, this confirms the administrative location where cross-domain trusts would be managed in an enterprise environment.

*(📸 Screenshots to add: Active Directory Domains and Trusts tool, Properties > Trusts tab)*
