# Command Snippets — Lab 4 (Ownership, Groups, Permissions & SUID)

> Safe, sanitized command snippets derived from Lab 4.  
> **Important:** Replace placeholders (`<...>`) locally. Never publish sensitive system files or private data.

---

## 1) Inspect permissions & ownership
```bash
# long listing with owner, group, and permissions
ls -l /path/to/file_or_dir

# show detailed inode/permission info
stat /path/to/file

# show first 200 entries in a directory listing
ls -l /etc | sed -n '1,200p'

2) Change owner and group (chown / chgrp)
  # change owner to 'alice' and group to 'devs' for a file
  sudo chown alice:devs /path/to/file
  
  # change group only
  sudo chgrp devs /path/to/file
  
  # change owner/group recursively for a directory
  sudo chown -R alice:devs /path/to/directory

3) Modify permissions with chmod (symbolic & numeric)
    # give owner read/write/execute, group read/execute, others read/execute (numeric)
  chmod 0755 /path/to/executable
  
  # remove write for group and others (symbolic)
  chmod go-w /path/to/file
  
  # add execute for owner
  chmod u+x script.sh
  
  # set exact permissions symbolically
  chmod u=rwx,g=rx,o=rx /path/to/executable

4) SUID bit (set-user-ID) — setting, clearing, and checking
  # set SUID (owner's privileges used when executing)
  sudo chmod u+s /path/to/executable
  
  # remove SUID
  sudo chmod u-s /path/to/executable
  
  # numeric form to set SUID + rwxr-xr-x => 4755
  sudo chmod 4755 /path/to/executable
  
  # check for SUID in ls -l output: an 's' appears in owner-exec position
  ls -l /path/to/executable
  # sample output: -rwsr-xr-x 1 root root ... indicates SUID set

5) Group checks & membership
  # show current user and groups
  id
  
  # list groups a user belongs to
  groups username
  
  # add a user to a group (requires root)
  sudo usermod -aG groupname username
  
  # show /etc/group entries for a given group
  getent group devs

6) ACLs (if available) — fine-grained permissions
  # view ACLs
  getfacl /path/to/file
  
  # set a user ACL (grant 'alice' read permission)
  sudo setfacl -m u:alice:r /path/to/file
  
  # remove an ACL
  sudo setfacl -x u:alice /path/to/file

7) Safe evidence collection & redaction (local only)
# save permission snapshot for a directory (safe sample)
ls -l /path/to/dir > ~/lab_evidence/perm_snapshot.txt

# redact sensitive lines before sharing (example: replace usernames)
sed -e 's/realuser/REDACTED_USER/g' ~/lab_evidence/perm_snapshot.txt > ~/lab_evidence/perm_snapshot_redacted.txt

# compress for local archiving
tar -czf ~/lab_evidence_lab04.tar.gz -C ~/lab_evidence .

8) Quick examples demonstrating SUID behavior (lab-only)
  # as root: create a test binary or script (compiled C example preferred),
  # set owner=root, set SUID, and run as an unprivileged user to observe effective UID.
  # NOTE: on many systems, SUID on scripts is ignored; use a small C program instead.
  
  # compile a tiny C program that prints uid/gid (lab VM example)
  cat > suid_test.c <<'C'
  #include <stdio.h>
  #include <unistd.h>
  int main() {
      printf("Real UID: %d\n", getuid());
      printf("Effective UID: %d\n", geteuid());
      return 0;
  }
  C
  gcc -o suid_test suid_test.c
  
  # set owner to root and set SUID (lab VM, requires sudo/root)
  sudo chown root:root suid_test
  sudo chmod 4755 suid_test
  
  # run as an unprivileged user and observe EUID showing root
  ./suid_test
  
