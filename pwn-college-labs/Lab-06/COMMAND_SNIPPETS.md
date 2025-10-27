# Command Snippets — Lab 5 (Permissions, SUID, `su`, `newgrp`)

> Safe, sanitized command snippets from Lab 5 workflows.  
> **Important:** Replace placeholders (`<...>`) locally. Never commit real flags, private passwords, or `/etc/shadow` extracts to public repos. Source: lab notes. :contentReference[oaicite:2]{index=2}

---

## 1) Inspecting a file's permissions & ownership
```bash
# long listing with owner/group and permissions
ls -l /flag

# detailed inode/permissions info
stat /flag

# list attributes for a directory (first 200 lines)
ls -l /tmp | sed -n '1,200p'

2) Reading the flag (when you are owner or file is readable)
# if you are owner and file is readable
cat /flag

# if file copied to /tmp and readable by you
cat /tmp/flag

3) Fixing overly-restrictive modes when you are the owner
# set SUID on a binary (lab-only; demonstrates effect)
sudo chmod u+s /bin/cat

# numeric equivalent (SUID + rwxr-xr-x)
sudo chmod 4755 /bin/cat

# check the permissions for 's' in the output
ls -l /bin/cat
# -rwsr-xr-x indicates SUID (owner exec shows 's')

4) Setting and inspecting SUID (demonstration in lab VM only)
# set SUID on a binary (lab-only; demonstrates effect)
sudo chmod u+s /bin/cat

# numeric equivalent (SUID + rwxr-xr-x)
sudo chmod 4755 /bin/cat

# check the permissions for 's' in the output
ls -l /bin/cat
# -rwsr-xr-x indicates SUID (owner exec shows 's')

5) Copying a protected file using elevated cp (lab scenario)
# copy protected file to a location you can read (example)
# this assumes the cp binary is running with elevated privileges in the lab
/bin/cp /flag /tmp/flag
ls -l /tmp/flag
cat /tmp/flag

6) Switching group with newgrp (interactive)
# change primary group to 'group_pvblrdcc' (you will be prompted for the group's password)
newgrp group_pvblrdcc

# after successful newgrp, verify primary group
id

# now attempt to read group-readable file
cat /flag

7) Switching user with su (interactive)
# switch to another user (prompts for the user's password)
su someuser

# run a single command as that user and return
su -c 'id; whoami' someuser

8) Identifying correct user/group (investigation steps)
# show current user and groups
whoami
id

# list group members for 'somegroup'
getent group somegroup

# search /etc/group for likely groups (sanitized)
grep 'group_p' /etc/group || true

9) Searching for hidden flags in /tmp (lab-only safe pattern)
# list recent /tmp directories (lab-only)
ls -ld /tmp/* | sort -k6,7

# search for files with 'tmp' pattern (do not read arbitrary files; only read lab-owned ones)
find /tmp -maxdepth 2 -type f -name 'tmp*' -ls | sed -n '1,200p'

10) Evidence collection (local only — sanitize before sharing)
# collect permission snapshots (redact before publishing)
ls -l /flag > ~/lab_evidence/flag_perm.txt
id > ~/lab_evidence/id.txt
groups > ~/lab_evidence/groups.txt

# redact usernames before committing public artifacts
sed -e 's/realuser/REDACTED_USER/g' ~/lab_evidence/flag_perm.txt > ~/lab_evidence/flag_perm_redacted.txt
