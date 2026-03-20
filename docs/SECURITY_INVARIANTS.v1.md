# CANONICAL SOURCE

# SECURITY_INVARIANTS v1

Status: **CANON**
Scope: Non-negotiable invariants for the guard system and its relationship to any protected system.

---

## Purpose

Define invariants so that:

- The guard cannot become a second decision authority.
- Fail-closed and deny-by-default apply to security evaluation, not only to the protected system's internal logic.
- Breach and tamper states are definable for audit and incident response.

---

## Invariants

**SI-1 — Fail-closed evaluation**
Any failure in the protected system's safety evaluation (import error, exception, missing module, invalid internal state) must result in the protected system's most restrictive state, never a permissive fallback. The guard must detect and alert on permissive-fallback conditions as CRITICAL.

**SI-2 — Artifact tamper-evidence**
The protected system's decision artifacts must be treated as append-only by operational policy. Cryptographic tamper-evidence (hash chain, signatures, or equivalent) is recommended. Until implemented, integrity is procedural and monitoring-based, not mathematically provable. The guard must monitor for artifact shrinkage, truncation, or unexpected modification.

**SI-3 — Secrets and version control**
Secrets (API keys, bot tokens, signing keys) must not appear in version-controlled source or configuration. Operational values must live only in non-committed files or a secret manager with restrictive filesystem permissions. The guard should scan for secret patterns in tracked files.

**SI-4 — Execution path observability**
Any live path from intent to external action in the protected system must be explicitly documented, gated by contract, and externally observable (logs, metrics, or artifacts). Hidden or parallel execution paths are forbidden. The guard must be able to verify that observed execution matches documented paths.

**SI-5 — Safety mechanism baseline**
The protected system's safety mechanisms (blockers, gates, validators) must not be fully disabled in production without a documented, reviewed exception. The guard must detect and alert on "all safety mechanisms disabled" as a critical configuration state.

**SI-6 — Guard has no decision authority**
The guard must not alter: the protected system's decision logic, permission verdicts, risk computation, eligibility semantics, or artifact content — except where a separate canonical contract explicitly allows a boundary-only action (see [SECURITY_BOUNDARY.v1.md](SECURITY_BOUNDARY.v1.md)).

**SI-7 — Detection vs enforcement separation**
Detection (observe, verify, alert) must be separable from enforcement (quarantine, block). Enforcement actions must be enumerated by mode in [MODE_CONTRACT.v1.md](MODE_CONTRACT.v1.md). Unlisted enforcement is forbidden.

---

## Relationship to other documents

| Document | Role |
|----------|------|
| [PROJECT_DISCIPLINE.v1.md](PROJECT_DISCIPLINE.v1.md) | Fail-closed operational law |
| [SECURITY_BOUNDARY.v1.md](SECURITY_BOUNDARY.v1.md) | What the guard may do; modes; quarantine rules |
| [MODE_CONTRACT.v1.md](MODE_CONTRACT.v1.md) | Mode semantics and allowed transitions |
| [AUTHORITY_BOUNDARY.v1.md](AUTHORITY_BOUNDARY.v1.md) | Zone permissions and prohibitions |

---

## Change control

Any weakening of SI-1, SI-3, SI-4, or SI-6 requires a version bump and explicit alignment with SECURITY_BOUNDARY and MODE_CONTRACT.
