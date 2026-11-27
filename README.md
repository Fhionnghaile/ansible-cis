# ansible-cis - CIS Level 1 hardening role

<!-- at-a-glance -->
> **Hardens a Linux host to the CIS Level-1 benchmark the same way, every time.**  
> **Result:** ansible-lint clean at the production profile; idempotent — a second run reports changed=0.  
> **Reproduce:** `ansible-lint   # idempotence: run the role twice; the 2nd run changes nothing`  
> ![CI](https://github.com/fhionnghaile/ansible-cis/actions/workflows/ci.yml/badge.svg) [![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/Fhionnghaile/ansible-cis/badge)](https://scorecard.dev/viewer/?uri=github.com/Fhionnghaile/ansible-cis)
>
> **What this is worth:** Applies the same CIS baseline to every host, and re-runs safely on a schedule (a second run changes nothing) to stop drift.


An **idempotent** Ansible role that hardens a Debian/Ubuntu host to a **CIS Level 1** profile, plus a
compliance playbook that emits a **before/after pass-fail report**.

```bash
ansible-galaxy collection install -r requirements.yml
ansible-playbook playbooks/harden.yml          # apply hardening (run twice -> zero changes = idempotent)
ansible-playbook playbooks/compliance.yml      # -> /tmp/cis-compliance-report.md
```

## Controls
Unused filesystems (1.1) - SSH daemon (5.2) - password policy (5.3/5.4) - auditd + rules (4.1) -
network sysctls (3.x) - host firewall (3.5). Each group toggles via `roles/cis_hardening/defaults/main.yml`.

## Quality
`ansible-lint` (production profile) + `yamllint` + `--syntax-check` run clean in CI; idempotence is
verified by a second converge producing zero changes.

## License
MIT.

## Key decisions

- Idempotent by construction, so it doubles as drift-correction, not just first-time setup.
- Built-in modules and namespaced vars only — no external dependencies to break on someone else's machine.
- Emits a compliance report, so the run is also an audit artifact.

## Scope & limits

- CIS Level 1 (the broad baseline); Level 2 and host-specific exceptions are deployment choices.
- Hardening can break bespoke apps — test against your workload before enforcing.

