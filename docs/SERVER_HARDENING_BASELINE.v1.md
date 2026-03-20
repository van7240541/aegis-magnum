# CANONICAL SOURCE

# SERVER_HARDENING_BASELINE v1

**Scope:** Baseline host and network posture for servers that may run a protected system, Aegis guard processes, or supporting services. **System-agnostic:** no requirement to use a specific Linux distribution; principles apply broadly.

This document is **policy**, not a generic checklist: each section states **required posture** for production-class hosts unless a written exception is recorded (risk acceptance). Vague “we use SSH” without the rules below is **non-compliant** with this baseline.

### Policy summary

| Policy | Requirement |
|--------|----------------|
| **Network default** | Deny-by-default; only explicitly allowed ports/sources. |
| **SSH** | Key-based login; password auth off for SSH; **no direct root login**. |
| **Privilege** | Least privilege for services and humans; separate accounts per role where practical. |
| **Patching** | Security patches applied on a defined cadence; reboot policy documented. |
| **Logging** | Auth, sudo, and service health retained and reviewable. |

---

## 1. SSH policy

- **Key-based authentication** for interactive access; **disable password authentication** for SSH (policy: passwords off, not “where feasible” as a permanent state).
- **Disable direct root login** over SSH; use unprivileged account plus `sudo` with logging.
- **Strong keys** (modern algorithms); avoid legacy weak ciphers where configurable.
- **Optional:** allowlist source IPs if operators have stable addresses (reduces brute-force noise).

---

## 2. Firewall

- **Default deny** inbound; allow only ports required for the workload (e.g. SSH from known sources only).
- **Outbound:** restrict egress where policy allows (defense in depth); document exceptions.
- Document rules so they are reproducible (infrastructure-as-code or runbook), not only “configured once by hand” without record.

---

## 3. Patching

- Enable **automatic security updates** for the OS where supported and tested.
- **Reboot policy:** define whether security kernels require planned reboot windows.
- Track critical CVEs affecting installed stack between patch cycles.

---

## 4. Service minimization

- Disable or remove unused services and daemons.
- Run application workloads under **dedicated service accounts** with minimal filesystem permissions.
- Prefer **separate users** for distinct roles (e.g. guard vs. application runtime) on the same host when co-located.

---

## 5. Mandatory access control (optional but recommended)

Where available (e.g. AppArmor, SELinux), apply profiles that constrain application capabilities beyond Unix permissions.

---

## 6. Brute-force and abuse mitigation

- Consider rate-limiting or lockout for SSH (e.g. fail2ban or equivalent) where appropriate.
- Monitor repeated failed authentication attempts.

---

## 7. Logging baseline

Retain and review:

- **Authentication:** SSH success/failure, sudo usage.
- **System:** service starts/stops, OOM, kernel errors.
- **Application / guard:** structured logs to append-only or rotated files as appropriate.

Centralized log shipping is recommended for multi-host setups; minimum is local retention with protected access.

---

## 8. Admin separation

- Avoid a **single shared** root password or shared sudo-capable account for all humans.
- **MFA** on cloud, Git, email, and provider panels where available — reduces account takeover chaining to SSH.

---

## 9. Relationship to Aegis

Aegis processes should run with **least privilege**: able to read configured artifact paths and emit alerts, without broad write access to protected application trees unless explicitly required by a future contract.

---

**Version:** v1
