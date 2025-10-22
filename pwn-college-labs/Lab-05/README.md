# 🛠️ Lab 4 — Perceiving Permissions (Ownership, Groups, & SUID)

**Name:** Carlos Rodriguez  
**Course:** CSCI 400 (Section 01)  
**pwn.college Username:** Carlos  
**Date:** 09/10/25  
**Source:** Original lab notes and screenshots (sanitized).

---

## 🎯 Objective
This lab focuses on Linux file ownership, group permissions, and special permission bits (notably the SUID bit). The goal was to understand how ownership and permission bits affect file execution and access, practice safely modifying permissions and owners in a sandboxed environment, and observe how the SUID bit changes runtime privileges for executables.

> **Sanitization note:** All artifacts here are redacted. Never publish real `/etc/shadow`, private keys, or unredacted system-sensitive files.

---

## 🧩 Topics Covered
- Changing file ownership: `chown` and `chgrp` workflows.  
- Group membership and how it affects file access.  
- Permission notation: symbolic (`rwx`) and numeric (`0755`) modes.  
- Executable file behavior and how `chmod` controls execution.  
- Permission tweaking practice — combining `chmod`, `chown`, umask considerations.  
- The **SUID** (set-user-ID) bit: how it makes executables run with the file owner's privileges and why it must be used cautiously.

---

## 🧰 Tools & Commands Practiced
- `ls -l`, `stat` — examine ownership and permission bits  
- `chown`, `chgrp` — change owner and group of files/directories  
- `chmod` (symbolic and numeric) — change permission bits, including SUID (`u+s`)  
- `getfacl` / `setfacl` (if available) — view and set ACLs for fine-grained access control  
- `id`, `groups` — inspect user and group membership

---

## ✅ Key Takeaways
- Ownership + group + permission bits together determine who can read, write, or execute a file.  
- The numeric permission model (e.g., `0755`) is a concise way to set `rwx` bits; symbolic notation (e.g., `u+rwx,g+rx,o+rx`) is more readable for small edits.  
- The SUID bit (`u+s`) causes an executable to run with the file owner's effective UID; this can be useful in controlled cases (e.g., `passwd` historically) but it is a significant security risk if misused.  
- Always sanitize and redact outputs if publishing results — permissions can leak information about system structure.

---

## 📁 Files in this Folder
lab-04/
├── Carlos-Rodriguez-Lab04.pdf # Full sanitized lab report (screenshots included)
├── README.md # This summary file
└── COMMAND-SNIPPETS.md # Copy-ready safe command snippets

---

⭐ *This lab strengthened my practical understanding of UNIX permissions and the security implications of special bits like SUID — essential for both system administration and secure coding practices.*
