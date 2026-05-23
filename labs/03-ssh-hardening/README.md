# Lab 03 — SSH Hardening

## Objective

This lab documents a basic SSH hardening workflow for a Linux server in a controlled lab environment. The goal is to reduce common remote-access risk while preserving administrative access.

## Baseline Review

| Check | Command | Purpose |
|---|---|---|
| SSH service status | `systemctl status ssh` | Confirm SSH is installed and running. |
| Listening ports | `ss -tulpn | grep ssh` | Confirm which port is listening. |
| Current configuration | `sudo sshd -T` | View effective SSH daemon settings. |
| Recent authentication | `sudo journalctl -u ssh --since "24 hours ago"` | Review recent SSH activity. |

## Recommended Controls

| Control | Example Setting | Security Reason |
|---|---|---|
| Disable root login | `PermitRootLogin no` | Reduces direct administrative login exposure. |
| Prefer key authentication | `PubkeyAuthentication yes` | Reduces password-based brute-force risk. |
| Disable password authentication after keys are tested | `PasswordAuthentication no` | Prevents password guessing over SSH. |
| Limit users | `AllowUsers oscar` | Restricts SSH access to approved accounts. |
| Reduce idle sessions | `ClientAliveInterval 300` and `ClientAliveCountMax 2` | Disconnects abandoned sessions. |
| Install fail2ban | `sudo apt install fail2ban` | Blocks repeated failed login attempts. |

## Safe Implementation Notes

Before disabling password authentication, confirm that key-based login works from a separate terminal session. Do not close the original session until the new login method is verified.

## Example Workflow

```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup
sudo nano /etc/ssh/sshd_config
sudo sshd -t
sudo systemctl reload ssh
sudo sshd -T | egrep 'permitrootlogin|passwordauthentication|pubkeyauthentication|allowusers'
```

## Validation

| Validation Step | Expected Result |
|---|---|
| Run `sudo sshd -t` | No syntax errors. |
| Attempt key-based login | Login succeeds for approved account. |
| Attempt root login | Login is denied. |
| Review logs | SSH log entries show successful and failed attempts. |
| Trigger repeated failures in lab | fail2ban detects and blocks repeated failures if configured. |

## Defensive Value

SSH hardening helps reduce the attack surface for brute-force attempts and credential misuse. From a SOC perspective, SSH logs also provide useful evidence for suspicious-login investigations.

## Lessons Learned

The key lesson is that hardening must be paired with validation. A secure configuration that locks out administrators creates an availability problem, while an unvalidated configuration creates a false sense of security.
