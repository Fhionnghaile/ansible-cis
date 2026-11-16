# cis_hardening

Idempotent Ansible role applying **CIS Level 1** controls to Debian/Ubuntu: unused-filesystem
blocks, SSH daemon hardening, password policy, auditd + rules, network sysctls, and a host firewall.

Each control group is toggle-able via `defaults/main.yml`. Pairs with `playbooks/compliance.yml`
which produces a **before/after pass-fail report**.
