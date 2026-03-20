# CANONICAL SOURCE

# SECURITY_BOUNDARY v1

Status: **CANON**
Scope: Defines what the guard system may and may not do when attached to a protected system. This is the primary capability contract.

---

## 1. Authority rule (non-negotiable)

The guard system does not participate in:

- Interpreting the protected system's domain data into decisions
- Permission or eligibility verdicts within the protected system
- Risk or safety computation that the protected system uses for its own authority
- Writing or rewriting the protected system's runtime artifacts except where this contract explicitly allows a single quarantine mechanism (see [QUARANTINE_CONTRACT.v1.md](QUARANTINE_CONTRACT.v1.md))

Violation of this rule turns the guard into a second opaque decision layer and is out of canon.

---

## 2. Detection vs enforcement

| Layer | Meaning | Allowed in v1 |
|-------|---------|---------------|
| **Detection** | Observe inputs, read artifacts, compute checks | Yes (default) |
| **Enforcement** | Cause the protected system or host to change behavior | Restricted — only modes in [MODE_CONTRACT.v1.md](MODE_CONTRACT.v1.md) |

All enforcement must be traceable to an explicit mode and audit record.

---

## 3. Read path (what the guard may do without additional contracts)

The guard may:

- **Observe**: tail or poll the protected system's artifact files, journals, health outputs, service status, process list, version control state — all read-only, as defined by the adapter.
- **Verify**: schema checks, cross-field consistency, integrity checks (hash chain when available), invariant conformance against copies or streams of the protected system's artifacts.
- **Alert**: notify operators via channels independent of the protected system's own alerting identity where possible (separate bot, webhook, or email) to prevent single-channel compromise.

The guard must not:

- Modify the protected system's source code, runtime scripts, or configuration.
- Inject or edit lines inside the protected system's artifact files.
- Set environment variables for the protected system's running processes.
- Forge entries in the protected system's event or intent streams.

---

## 4. Minimum enforcement discipline (alerts)

When verification fails, the guard must at minimum:

| Condition | Minimum response |
|-----------|-----------------|
| Artifact integrity check failed (shrinkage, broken chain) | ALERT (high); recommend human investigation |
| Protected system's fail-closed invariant violated | ALERT CRITICAL |
| Secret material detected in version-controlled source | ALERT CRITICAL; recommend credential rotation |

This section defines minimum alert obligations. It does not grant automatic quarantine.

---

## 5. Universal product shape

For reuse beyond any single protected system:

- **Core (generic)**: file/process monitoring, optional secret scanning, configuration validation hooks, alerting adapters, audit logging.
- **Adapter (system-specific)**: artifact schemas, join keys, mapping to the protected system's invariants, quarantine mechanism path and payload shape.

The core must default to OBSERVE + VERIFY + ALERT only. QUARANTINE requires explicit configuration and a canonical contract. BLOCK requires a future enforcement contract.

---

## 6. References

- [SECURITY_INVARIANTS.v1.md](SECURITY_INVARIANTS.v1.md)
- [MODE_CONTRACT.v1.md](MODE_CONTRACT.v1.md)
- [QUARANTINE_CONTRACT.v1.md](QUARANTINE_CONTRACT.v1.md)
- [AUTHORITY_BOUNDARY.v1.md](AUTHORITY_BOUNDARY.v1.md)
- [ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md)

---

## Change control

New enforcement powers (especially BLOCK) require a new version of this document or a child contract referenced here. Expanding quarantine beyond the adapter-defined mechanism requires the same.
