# 🔐 Lab 5 — File Permissions & User/Group Privilege Workflows

**Name:** Carlos Rodriguez  
**Course:** CSCI 400 (Section 01)  
**pwn.college Username:** Carlos  
**Date:** 09/13/25  
**Source:** Original lab notes and screenshots (sanitized).

---

## 🎯 Objective
This lab explores UNIX file permissions, ownership, group privileges, SUID behavior, and basic account switching (`su`, `newgrp`). Through a sequence of challenge levels, I practiced how permissions restrict access and how authorized user/group changes and special bits enable or prevent reading protected files.

> **Sanitization:** All published artifacts are redacted. Do not include real flags, unhashed passwords, or unredacted shadow files.

---

## 🧩 Summary of Levels (1–12)
- **Level 1–2:** Investigated `/flag` files set to `0400` (owner-read only). Verified ownership and used `cat /flag` once ownership was confirmed.  
- **Level 3:** Encountered a `/flag` with `000` permissions; resolved by (as owner) changing permissions (e.g., `chmod 400 /flag`) then reading it.  
- **Level 4:** Observed how **SUID** affects runtime privileges — setting SUID on `/bin/cat` caused it to run with the file owner's privileges (root in the lab), allowing `/bin/cat /flag`.  
- **Level 5:** Demonstrated that `cp` can inherit elevated privileges when run with SUID-root binary (e.g., `/bin/cp /flag /tmp/flag`) enabling reading the copy.  
- **Level 6:** Joined a specific group (`group_pvblrdcc`) using `newgrp` with the provided password; group membership allowed reading a group-protected flag.  
- **Levels 7–10:** Practiced switching to newly created users (`su username`) and verifying world-readable or group-readable permissions to access flags. Identified the correct user/group when multiple accounts exist.  
- **Levels 11–12:** Performed chained user switches across multiple accounts to navigate tiered restrictions (e.g., moving through users to access nested `/tmp` directories and the secret file).

---

## 🧰 Tools & Concepts Practiced
- `ls -l`, `stat` — inspect permissions and ownership  
- `chmod` / `chown` / `chgrp` — modify permissions and ownership (when authorized)  
- SUID behavior (`chmod u+s`) and how it affects effective UID at runtime  
- `cp` behavior when executed with elevated privileges  
- `su` and `newgrp` — switching user contexts and changing primary group interactively  
- Group membership inspection (`id`, `groups`, `getent group`)

---

## ✅ Key Takeaways
- File permissions (owner/group/other) and special bits (SUID) are fundamental to protecting resources.  
- Being the file owner allows corrective actions (e.g., `chmod`) even if the file has restrictive modes like `000`.  
- SUID on a trusted binary can be used to perform actions as another user — extremely powerful and must be carefully controlled.  
- `newgrp` is useful when a group has its own password in a lab environment; `su` lets you switch to other accounts to leverage their permissions.  
- When publishing lab results, always **sanitize** outputs (no flags, no passwords, no raw `/etc/shadow`).

---

## 📁 Files in this Folder
lab-05/
├── Carlos-Rodriguez-Lab05.pdf # Full sanitized lab report (screenshots included)
├── README.md # This summary file
└── COMMAND-SNIPPETS.md # Copy-ready safe command snippets

---

⭐ *This lab deepened my practical understanding of UNIX permission models and how account/group changes and special permission bits control access to protected resources.*
