# Lab 05 — Linux Firewall Basics

## Objective

This lab template documents a host-based firewall baseline using UFW or iptables in a controlled Linux lab environment.

## UFW Baseline Commands

| Goal | Command |
|---|---|
| Check status | `sudo ufw status verbose` |
| Default deny inbound | `sudo ufw default deny incoming` |
| Default allow outbound | `sudo ufw default allow outgoing` |
| Allow SSH from trusted source | `sudo ufw allow from <trusted_ip> to any port 22 proto tcp` |
| Enable firewall | `sudo ufw enable` |
| Review numbered rules | `sudo ufw status numbered` |

## Analyst Notes

Firewall rules should be specific, documented, and validated. In a real environment, firewall changes require approval and rollback planning.
