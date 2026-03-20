# CANONICAL SOURCE

# CANON_CORE_FOR_AUDIT v1

Status: **CANON**
Purpose: Single reference supplying Definitions, Invariants, Prohibitions, Versioning, and Document Precedence for architectural audit. No interpretation — citations and pointers only. If a claim is not grounded here or in the linked binding artifacts, it is not canon.

---

## 1. Definitions

### 1.1 Guard system domains

- **Core**: Universal guard engine — monitoring, verification, alerting, policy evaluation, audit logging. Domain-agnostic. No knowledge of any specific protected system.
- **Adapter**: Project-specific integration layer. Knows the protected system's artifact layout, invariants, process identity, and quarantine mechanism. Implements the interface defined in [ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md).
- **Channel**: Alert delivery — Telegram, webhook, email, stdout. Independent from the protected system's own notification channels.
- **Governance**: Canonical documents, contracts, and configuration that define rules. Not part of the live compute path.

### 1.2 Mode vocabulary

Defined in [MODE_CONTRACT.v1.md](MODE_CONTRACT.v1.md):

- **OBSERVE** — read-only telemetry (default)
- **VERIFY** — checks and internal scoring; no outbound action
- **ALERT** — emit notifications on failed checks
- **QUARANTINE** — request boundary restriction via the protected system's mechanism
- **BLOCK** — interpose on protected system's execution path; forbidden until separate enforcement contract exists

### 1.3 Status labels

Every document in this repository carries one of:

- **CANONICAL SOURCE** — binding; defines rules, contracts, or invariants
- **NON-CANONICAL DRAFT** — informational; informs decisions but has no architectural authority
- **EXPORT BOOTSTRAP** — temporary scaffolding for repository setup; to be promoted or removed

---

## 2. Invariants

Defined in [SECURITY_INVARIANTS.v1.md](SECURITY_INVARIANTS.v1.md). Summary:

- **SI-1**: Protected system's fail-closed evaluation must not degrade to permissive state on failure.
- **SI-2**: Artifacts must be treated as append-only; tamper-evidence is required when feasible.
- **SI-3**: Secrets must not appear in version-controlled source.
- **SI-4**: Execution paths in the protected system must be externally observable.
- **SI-5**: Safety mechanisms in the protected system must have a minimum enforced baseline.
- **SI-6**: The guard must not hold decision authority over the protected system.
- **SI-7**: Detection and enforcement must be separable.

---

## 3. Prohibitions

The guard system MUST NEVER:

- **P-1**: Alter the protected system's decision logic, permission verdicts, or risk computation.
- **P-2**: Write to, edit, or forge entries in the protected system's runtime artifacts.
- **P-3**: Set environment variables or configuration for the protected system's running processes.
- **P-4**: Acquire enforcement capability without an explicit versioned contract.
- **P-5**: Operate in BLOCK mode without a separate enforcement contract.
- **P-6**: Re-apply quarantine on a timer without operator visibility.
- **P-7**: Use the protected system's own alerting channel as its sole notification path.

---

## 4. Versioning

- Canonical documents carry version suffixes (e.g. `.v1.md`).
- Semantic changes (new invariants, relaxed prohibitions, expanded authority) require a **version bump**.
- Non-semantic changes (typo fixes, clarifications that do not alter meaning) may be made in-place.
- A frozen document may not be changed; a new version must be created.

---

## 5. Document precedence

When documents conflict, the binding order is:

1. SECURITY_INVARIANTS.v1.md
2. SECURITY_BOUNDARY.v1.md
3. MODE_CONTRACT.v1.md
4. QUARANTINE_CONTRACT.v1.md
5. AUTHORITY_BOUNDARY.v1.md
6. PROJECT_DISCIPLINE.v1.md
7. ADAPTER_CONTRACT.v1.md
8. All other canonical documents

Higher-precedence restrictions override lower-precedence permissions.

---

## Change control

Any weakening of invariants or prohibitions listed here requires a version bump of this document and explicit alignment with SECURITY_INVARIANTS and SECURITY_BOUNDARY.
