# 🧭 Lab 2 — Dealing with Data & Intro to Cryptography

**Name:** Carlos Rodriguez  
**Course:** CSCI 400 (Section 01)  
**pwn.college Username:** Carlos  
**Dojo Links:**  
- Dealing with Data — https://pwn.college/fundamentals/data-dealings/  
- Cryptography — https://pwn.college/intro-to-cybersecurity/cryptography/  
**Source:** Original lab report (sanitized). :contentReference[oaicite:0]{index=0}

---

## 🎯 Objective
This lab explores safe data handling and introductory cryptographic techniques in the pwn.college sandbox. Tasks included reading challenge programs to discover expected inputs, handling different encodings (binary/hex, Base64), and applying basic cryptographic primitives and reasoning (XOR, AES, RSA, DHKE, hashing). All published artifacts are sanitized — no flags or sensitive payloads are included.

---

## 🧩 Lab Sections & Key Tasks

### **Part A — Dealing with Data**
(Foundational tasks about how challenge programs consume input)
- Inspect challenge binaries / scripts (e.g., `/challenge/runme`) to find hard-coded passwords instead of guessing.  
- Handle newline/input quirks (e.g., use `Ctrl+D` or `echo -n` to avoid a trailing newline).  
- Provide input via files when the program reads from a filename (create `xthd` or provide filename as a command-line argument).  
- Understand byte vs. text input: submit hex (`fromhex`) when required and convert raw bytes appropriately.  
- Extract and decode embedded Base64 data found inside challenge files.

**Representative approaches used:**
- `cat /challenge/runme` to read challenge source (when allowed).  
- `echo -n "password" > filename` to create file inputs without newline.  
- `python -c 'import base64; print(base64.b64encode(b"\xf0\x06..."))'` for encoding tasks.  

---

### **Part B — Cryptography Fundamentals**
(Hands-on practice with small crypto primitives)
- **XOR / XORing Hex / XORing ASCII:** apply XOR with given keys to reveal plaintexts; implement small scripts to iterate through rounds.  
- **One-Time Pad & Tampering:** convert hex to raw bytes and XOR with key bytes; attempted tampering approaches to flip ciphertext to a target plaintext (some sub-tasks blocked by missing executables in the sandbox).  
- **AES (AES-128 ECB):** convert hex ciphertext to raw bytes and decrypt with OpenSSL or Python to recover plaintext.  
- **Diffie–Hellman Key Exchange (DHKE):** replicate p, g, and public values; compute private key, corresponding public B, and shared secret s.  
- **RSA (practice):** raise ciphertext to the private exponent modulo n; examine raw bytes for padding/structure; attempted various unpadding strategies (PKCS#1 v1.5 / OAEP) but challenge-specific encoding/padding may require additional steps.  
- **Hashing / Partial-Collision (SHA-256 prefix):** implemented brute-force strategies (single-core, parallel, batched) and one-shot scripts to (1) launch the challenge, (2) parse the required prefix, and (3) target the running process. Verified input format required HEX-encoded bytes rather than raw/base64; noted performance/time constraints for finding 24-bit prefix collisions.

---

## 🧰 Tools & Commands Practiced
- `cat`, `echo -n`, basic shell utilities  
- Python for quick byte/encoding work (`base64`, `binascii`, simple XOR loops)  
- OpenSSL CLI for AES decryption: `openssl enc -d -aes-128-ecb -K <hexkey> -in <cipher.bin>`  
- Small brute-forcers using multiprocessing / parallel strategies for hash-prefix search  
- Basic RSA modular exponentiation routines (Python `pow(c, d, n)`)

---

## ✅ Key Learnings & Notes
- Inspect challenge code when possible — many “puzzles” simply require reading the program to learn the expected input format.  
- Be careful with input formats: many challenges expect **HEX-encoded bytes**, not literal text or base64; `fromhex()` vs. raw ASCII matters.  
- For timed/compute-heavy tasks (e.g., SHA-256 prefix collision), parallelization and adequate CPU resources are crucial — sandbox VMs may be too limited to finish within a deadline.  
- Cryptography exercises often depend on correct padding/encoding choices in addition to correct math (RSA decryption may yield raw bytes requiring specific unpadding or decoding to retrieve a human-readable flag).  
- Document failed attempts and environment issues (e.g., missing executables) — these are valuable learning artifacts.

---

## ⚠️ Notes on Incomplete or Blocked Tasks
- One-time pad tampering: could not finish due to missing dispatcher/worker binaries in the challenge directory; scripted approaches were prepared but could not be validated.  
- SHA-256 partial-collision: method validated and working locally, but limited VM resources prevented completion before deadline; solution scales with more CPU cores/time.

---

## 📁 Files in this Folder
lab-02/
├── Carlos-Rodriguez-Lab02.pdf # Full sanitized lab report (screenshots included)
├── Santized command snippets
└── README.md # This summary file
