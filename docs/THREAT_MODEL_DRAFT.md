# NON-CANONICAL DRAFT

# THREAT_MODEL_DRAFT — Risk Assessment

Status: **NON-CANONICAL DRAFT**
Purpose: Structured risk assessment for a specific protected system. Does not drive guard design until reviewed and promoted. Every risk must reference a verified fact or explicitly state INFERRED.

---

## Status rule

This document is informational input for guard design. Risks listed here do not automatically become guard rules or invariants. Promotion path:

1. Risk must be grounded in a verified fact from [VERIFIED_FACTS.md](VERIFIED_FACTS.md) or explicitly marked INFERRED.
2. INFERRED risks cannot be used as basis for enforcement design (quarantine rules, alert policies).
3. Only VERIFIED current-state risks can drive guard invariants or adapter configuration.
4. Promotion requires creating or updating a canonical document that cites the risk ID.

---

## Section 1 — Current-state risks

Risks that exist now in the protected system's current configuration.

| ID | Threat | Category | Basis (fact ID or INFERRED) | Severity | Status |
|----|--------|----------|-----------------------------|----------|--------|
| T-CS-001 | (example: "Secret in version-controlled file") | Secret exposure | F-001 | CRITICAL | VERIFIED |

### Categories

- **Secret exposure**: tokens, keys, credentials accessible to unauthorized parties.
- **Permission bypass**: conditions that allow the protected system to skip safety checks.
- **Artifact tampering**: ability to modify decision/event history.
- **Privilege excess**: processes running with more permissions than needed.
- **Configuration drift**: ability to disable safety mechanisms without detection.
- **Code integrity**: ability to deploy unverified code changes.

---

## Section 2 — Future-state risks

Risks that do not exist now but will emerge when planned features are activated.

| ID | Threat | Category | Basis (fact ID or INFERRED) | Severity | Status |
|----|--------|----------|-----------------------------|----------|--------|
| T-FS-001 | (example: "Live execution path creates real financial exposure") | Execution safety | F-002 | CRITICAL | FUTURE-RISK |

---

## Section 3 — Inferred risks requiring verification

Risks based on reasonable inference but lacking direct evidence. These require live system access to confirm or deny.

| ID | Threat | Category | Basis | What to verify | Status |
|----|--------|----------|-------|----------------|--------|
| T-INF-001 | (example: "Service may be running as root") | Privilege excess | No User= in service unit | Check process owner on live system | INFERRED |

---

## Usage rules

1. Every risk must reference a verified fact ID or state INFERRED. No unsupported claims.
2. INFERRED risks are hypotheses, not findings. They drive investigation, not design.
3. Severity levels: CRITICAL, HIGH, MEDIUM, LOW.
4. Status values: VERIFIED (evidence confirmed), INFERRED (hypothesis), FUTURE-RISK (not yet active).
5. This document should be re-assessed whenever the protected system changes significantly.

---

## Next steps

After populating this document:

1. For each INFERRED risk, create a corresponding entry in [OPEN_QUESTIONS.md](OPEN_QUESTIONS.md) to track verification.
2. For each VERIFIED CRITICAL risk, evaluate whether a guard invariant or alert rule should be created.
3. For each FUTURE-RISK, document the trigger condition (what change in the protected system activates this risk).
