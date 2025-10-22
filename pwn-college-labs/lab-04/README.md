# 🧭 Lab 3 — Privilege Basics: `su`, `sudo`, & Password Handling

**Name:** Carlos Rodriguez  
**Course:** CSCI 400 (Section 01)  
**pwn.college Username:** Carlos  
**Date:** 09/08/25  

---

## 🎯 Objective
This lab covers fundamental privilege-management concepts in Linux: switching users with `su`, inspecting and enumerating `sudo` privileges, and basic password-handling / cracking techniques used in controlled learning environments. The goal was to learn how privilege escalation is managed and to practice responsible investigative techniques in a sandbox.

> **Sanitization note:** All public artifacts are redacted for safety. Do not publish real password hashes, active user credentials, or live `/etc/shadow` files in public repos.

---

## 🧩 Topics Covered
- **Becoming root with `su`** — how `su` works, when it prompts for a password, and how shells are affected by `su -` vs `su <user>`.  
- **Other users with `su`** — safe workflow to switch to non-root accounts for testing permissions.  
- **Cracking Passwords (educational)** — overview of controlled offline password-cracking workflows (hash extraction in a sandbox, use of cracking tools for learning).  
- **Using `sudo`** — enumerating `sudo` capabilities (`sudo -l`), using `sudo` safely, and understanding the scope of allowed commands.

---

## 🧰 Skills Practiced
- Safe privilege switching (`su`, `sudo`) in sandboxed environments  
- Enumerating `sudo` rights and interpreting `sudo -l` output  
- Responsible handling of password hashes in an isolated lab (how to prepare sanitized test vectors; when not to publish)  
- Understanding how system accounts and group membership affect privilege

---

## ✅ Key Takeaways
- `su` hands you a new shell as another user; `su -` loads that user’s login environment.  
- `sudo -l` is a crucial reconnaissance step: it lists what actions the current user may run as root or other users.  
- Offline password cracking should **only** be performed on hashes you own or in sanctioned lab environments; never publish the raw `/etc/shadow` file.  
- Documentation and redaction are essential when sharing lab results — always remove real hashes and flags.

---

## 📁 Files in this Folder
lab-03/
├── Carlos-Rodriguez-Lab03.pdf # Full sanitized lab report (screenshots included)
├── README.md # This summary file
└── COMMAND-SNIPPETS.md # Copy-ready safe command snippets (see below)

---

⭐ *This lab reinforced practical, ethical handling of privileges and password artifacts — foundational skills for any security practitioner.*
