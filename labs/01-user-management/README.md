# Lab 01 — Linux User Management and Account Review

## Objective

This lab documents a basic Linux account review workflow. The goal is to identify local users, group membership, sudo privileges, locked accounts, and potential least-privilege concerns.

## Review Commands

| Goal | Command | Why It Matters |
|---|---|---|
| List local users | `cut -d: -f1 /etc/passwd` | Shows accounts present on the system. |
| Review login shells | `awk -F: '{print $1, $7}' /etc/passwd` | Identifies accounts with interactive shells. |
| Review sudo group | `getent group sudo` | Identifies users with administrative capability. |
| Review password status | `sudo passwd -S username` | Shows whether an account is locked or active. |
| Review recent logins | `last -a` | Shows interactive login history. |

## Analyst Notes

Account review is basic but important. A compromised or forgotten account can create unnecessary risk, especially if it has sudo access or an interactive shell.
