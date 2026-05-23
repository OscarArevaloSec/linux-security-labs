# Lab 02 — Linux File Permissions Review

## Objective

This lab template is used to document Linux file permission review. The focus is understanding ownership, access rights, and risky permissions.

## Review Areas

| Area | Command | Security Question |
|---|---|---|
| File permissions | `ls -la` | Who can read, write, or execute this file? |
| Ownership | `stat filename` | Who owns the file and group? |
| SUID files | `find / -perm -4000 -type f 2>/dev/null` | Are privileged execution bits present? |
| World-writable files | `find / -perm -002 -type f 2>/dev/null` | Can any user modify the file? |
| ACLs | `getfacl filename` | Are extended permissions configured? |

## Documentation Standard

For each finding, document the file path, owner, permissions, risk, and recommended change.
