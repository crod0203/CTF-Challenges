# 🧭 Lab 1 — Linux Paths

**Name:** Carlos Rodriguez  
**Course:** CSCI 400 (Section 01)  
**pwn.college Username:** Carlos  
**Dojo Link:** https://pwn.college/linux-luminarium/paths/  
**Source:** Original lab notes and screenshots (sanitized). :contentReference[oaicite:0]{index=0}

---

## 🎯 Objective
Practice navigating the Linux filesystem and become comfortable with absolute, relative, and special paths in a sandboxed CTF environment. This lab focuses on understanding how paths resolve from different working directories and how to locate challenge files and flags.

> **Note:** All artifacts in this public repo are sanitized — flags and any sensitive outputs are redacted.

---

## 🧩 Lab Sections & Tasks

### **Part 1 — Linux Luminarium: Paths**
[Dojo Link](https://pwn.college/linux-luminarium/paths/)  
Challenges completed:
- **The Root** — examine root directory structure and locate top-level files.  
- **Program and Absolute Paths** — practice referencing executables and files by absolute path.  
- **Position Thy Self / Position Elsewhere / Position Yet Elsewhere** — change working directories and confirm path resolution.  
- **Implicit Relative Paths (from /)** — understand how paths resolve when implied from root.  
- **Explicit Relative Paths (from /)** — use `.` and `..` to reference files relative to current directory.  
- **Implicit Relative Path** — practice commands that assume relative addressing.  
- **Home Sweet Home** — return to and operate within the home directory.

---

## 🧰 Tools & Commands Practiced
- `pwd`, `ls`, `cd` — directory navigation and inspection  
- Absolute vs relative path usage (`/path/to/file` vs `./file` / `../file`)  
- Understanding of special directories: `/`, `~`, `.`, `..`  
- Safe interaction with challenge executables (no exploit payloads published)  

---

## ✅ Key Learnings
- How absolute paths resolve regardless of the current working directory.  
- How relative paths depend on your current directory and when to use `.`/`..`.  
- Best practices for locating challenge files in nested directories.  
- Awareness of persistence and session state when using the pwn.college sandbox.

---

## 📁 Files in this Folder
