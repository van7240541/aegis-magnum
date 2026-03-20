# CANONICAL SOURCE

# INCIDENT_RESPONSE_AND_KEY_COMPROMISE v1

**Scope:** Minimal procedures when a secret is suspected leaked, a host is compromised, or guard/adapter behavior indicates boundary violation. **Operational detail** (exact commands) lives in runbooks; this canon defines **what must happen**, not vendor-specific steps.

---

## 1. Assume compromise is possible

Design and operations should assume **keys will eventually leak** or **accounts will be phished**. Response must be **fast and ordered**, not improvised.

---

## 2. Key leak — immediate actions

1. **Stop** using the leaked credential for new actions (do not rotate “in place” while attacker may still use old token).
2. **Revoke** at the source (GitHub, cloud API, exchange, bot API, SSH `authorized_keys`).
3. **Issue** replacement credentials with new material; never reuse the leaked secret string.
4. **Deploy** replacements to legitimate systems before deactivating old (overlap window as short as practical).
5. **Review** logs for unauthorized access in the exposure window — [SERVER_HARDENING_BASELINE.v1.md](SERVER_HARDENING_BASELINE.v1.md).
6. **Document** incident: what, when, scope, resolution — in operational tracking (not in git with secrets).

---

## 3. SSH or host compromise

1. **Isolate** the host from sensitive networks if ongoing abuse is suspected (firewall, provider console).
2. **Preserve** forensic evidence if investigation is required (snapshot, disk image — per policy).
3. **Rotate** all credentials that could have been read from that host (not only the one key suspected).
4. **Rebuild** from known-good baseline where root compromise is confirmed (patching alone may be insufficient).
5. **Review** user accounts, cron, systemd units, and unauthorized binaries.

---

## 4. Revoking access (people)

- Remove **Git org** access, **SSH keys**, **shared panels**, and **API tokens** tied to the person or role.
- Verify **MFA recovery** paths are not attacker-controlled (email forwarding, phone).

---

## 5. Rotating secrets (batch)

After a wide incident:

1. Inventory all secret types — [SECRETS_AND_KEY_MANAGEMENT.v1.md](SECRETS_AND_KEY_MANAGEMENT.v1.md).
2. Prioritize **highest blast radius** (cloud root, exchange, production DB).
3. Rotate in **dependency order** (e.g. revoke outbound tokens before deleting inbound acceptance if needed).
4. Verify each service after rotation.

---

## 6. Isolating components

- **Network:** segment so a compromised guard host cannot reach execution endpoints unnecessarily.
- **Credentials:** separate keys so revoking one does not require full platform downtime.
- **Aegis:** disabling the guard must not brick the protected system — see [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md).

---

## 7. Minimal recovery checklist

- [ ] Threat contained (revocation / isolation)
- [ ] Secrets rotated per inventory
- [ ] Logs reviewed for IOCs in window
- [ ] Services healthy on new credentials
- [ ] Incident record closed with lessons learned

---

## 8. Escalation

Define **who** is contacted for regulatory, legal, or customer notification per your jurisdiction and product — not specified in this canon.

---

**Version:** v1
