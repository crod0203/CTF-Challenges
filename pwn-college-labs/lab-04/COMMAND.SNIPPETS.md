# Command Snippets — Lab 3 (Privilege & Password Handling)

> Safe, sanitized command snippets derived from Lab 3 activities.  
> **Important:** Replace placeholders (`<...>`) locally. Never commit `/etc/shadow` or real password hashes to a public repo.

---

##1) Basic `su` usage (switch users)
```bash
  # switch to root (prompts for root password)
  su -
  
  # switch to a different user (prompts for that user's password)
  su - someuser
  
  # run a single command as another user (keeps your shell)
  su -c 'whoami; id' someuser
  
  # list allowed sudo commands for current user
  sudo -l
  
  # run an allowed command as root (if sudo -l showed it)
  sudo <allowed-command>
  
  # check which user you're running as
  whoami

3) Safe file/permission checks (no sensitive data)
  # list file ownership and permissions for /etc
  ls -l /etc | sed -n '1,120p'
  
  # inspect passwd (safe to view)
  cat /etc/passwd | sed -n '1,120p'
  
  # DO NOT cat /etc/shadow in public — requires root and contains sensitive hashes
  # cat /etc/shadow

4) Preparing a sanitized hash file for offline testing (example workflow)
  # (As root in lab only) extract a single user's passwd+shadow entry to a local test file (sanitized):
  # 1) get username line from /etc/passwd
  grep '^someuser:' /etc/passwd > /tmp/someuser_passwd

  # 2) get just the hash line from /etc/shadow (requires root) — SAVE LOCALLY & KEEP PRIVATE
  sudo grep '^someuser:' /etc/shadow > /tmp/someuser_shadow

  # 3) combine to create an "unshadow" input for john (john requires a combined file format)
  # The 'unshadow' utility usually pairs passwd+shadow into a john-friendly file
  sudo unshadow /tmp/someuser_passwd /tmp/someuser_shadow > /tmp/someuser_unshadow
5) Password-cracking (educational, single-user example using john)
  # run john against a local unshadow file (single-core example)
  john /tmp/someuser_unshadow --wordlist=/usr/share/wordlists/rockyou.txt --rules
  
  # show cracked passwords
  john --show /tmp/someuser_unshadow

6) Create/Change a local user's password (admin tasks)
    # change password for current user (interactive)
  passwd
  
  # change password for another user (requires root)
  sudo passwd someuser
  
  # set password non-interactively (for test VMs only; DO NOT use on shared systems)
  echo "someuser:NewP@ssw0rd" | sudo chpasswd
7) Check group membership & sudoers (investigation)
    # see groups for current user
  groups
  
  # check if a specific user is in 'sudo' or 'wheel' group
  getent group sudo
  getent group wheel
  
  # view /etc/sudoers (use visudo for edits)
  sudo visudo -c        # check sudoers syntax (safe)
8) Logging & evidence collection (sanitized)
  # collect system info (safe snapshot)
id > ~/lab_evidence/id.txt
uname -a > ~/lab_evidence/uname.txt
ps -ef | head -n 40 > ~/lab_evidence/ps.txt

# compress and keep local (do not upload sensitive logs)
tar -czf ~/lab_evidence.tar.gz -C ~/lab_evidence .


