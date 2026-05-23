# Linux Security Labs

This repository documents hands-on Linux administration and defensive security practice. The labs are written to show command-line work, security reasoning, and analyst-style documentation rather than only listing commands.

## Lab Index

| Lab | Topic | Primary Skills Demonstrated | Status |
|---|---|---|---|
| [01 User Management](labs/01-user-management/README.md) | Users, groups, sudo, account review | Account inventory, least privilege, basic audit workflow. | Drafted |
| [02 File Permissions](labs/02-file-permissions/README.md) | chmod, chown, SUID/SGID, ACLs | Permission review and risk explanation. | Template |
| [03 SSH Hardening](labs/03-ssh-hardening/README.md) | SSH configuration, key authentication, fail2ban | Secure remote access and brute-force reduction. | Drafted |
| [04 Log Analysis](labs/04-log-analysis/README.md) | auth.log, syslog, journalctl | Failed-login review and suspicious authentication triage. | Drafted |
| [05 Firewall Basics](labs/05-firewall-basics/README.md) | ufw, iptables, default-deny principles | Host firewall baseline and rule documentation. | Template |

## Environment

| Item | Detail |
|---|---|
| Operating system | Ubuntu 22.04 LTS or similar Linux lab VM. |
| Scope | Isolated home lab or virtual machine only. |
| Safety rule | Do not run hardening changes on production systems without approval and a rollback plan. |

## Documentation Standard

Each lab should include the objective, baseline state, commands used, explanation, validation, security impact, and lessons learned. A good lab explains why the command matters and how the result would help a defender.
