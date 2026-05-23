# Lab 04 — Linux Authentication Log Analysis

## Objective

This lab documents how to review Linux authentication logs for suspicious login activity. The goal is to practice blue-team analysis using evidence, timelines, and clear conclusions.

## Common Log Sources

| Log Source | Purpose |
|---|---|
| `/var/log/auth.log` | Debian/Ubuntu authentication events, sudo usage, SSH logins, and failed attempts. |
| `/var/log/secure` | RHEL/CentOS authentication and security events. |
| `journalctl -u ssh` | SSH service logs from systemd journal. |
| `last` | Recent successful logins. |
| `lastb` | Failed login attempts when enabled. |

## Useful Commands

| Goal | Command |
|---|---|
| View recent SSH logs | `sudo journalctl -u ssh --since "24 hours ago"` |
| Search failed passwords | `sudo grep "Failed password" /var/log/auth.log` |
| Search accepted logins | `sudo grep "Accepted" /var/log/auth.log` |
| Count failed login source IPs | `sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr` |
| Review sudo usage | `sudo grep "sudo" /var/log/auth.log` |
| Review recent logins | `last -a` |

## Analyst Questions

| Question | Why It Matters |
|---|---|
| Which user accounts were targeted? | Shows whether the attack was random or focused. |
| Which source IPs appear repeatedly? | Helps identify brute-force sources. |
| Was there a successful login after failures? | Increases suspicion and severity. |
| Was the account privileged? | Privileged access increases impact. |
| Did the login occur at an unusual time? | Adds behavioral context. |
| What happened after login? | Determines whether the activity caused impact. |

## Sample Finding Format

| Finding | Evidence | Severity | Recommendation |
|---|---|---|---|
| Repeated SSH failures against `admin` | 42 failures from one source IP in 10 minutes. | Medium | Disable unused account, block source IP, require key-based login, monitor for successful access. |
| Successful login after failures | Accepted login from same source after multiple failures. | High | Reset credentials, revoke sessions, review command history, escalate for deeper investigation. |

## Defensive Value

Authentication logs are one of the first places a SOC analyst may look during suspicious-login triage. This lab supports alert investigation, timeline creation, and evidence-based reporting.
