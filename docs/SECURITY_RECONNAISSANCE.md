# NON-CANONICAL DRAFT

# SECURITY_RECONNAISSANCE — Observation Registry

Status: **NON-CANONICAL DRAFT**
Purpose: Record verified and unverified observations about a protected system's attack surface before designing guard rules.

---

## Status rule

This document is informational. It informs guard design but has no architectural authority. Observations recorded here do not automatically become invariants or contracts. Promotion to canonical status requires:

1. Verification of each claim against the protected system's actual state.
2. Review by the guard system's owner.
3. Creation of a corresponding entry in a canonical document (invariant, boundary rule, or adapter spec).

---

## Structure

Each observation is recorded as a row in the table below.

| ID | Category | Claim | Evidence source | Verification method | Status |
|----|----------|-------|-----------------|---------------------|--------|
| R-001 | (example) | (description of what was observed) | (file:line, command output, config entry) | (how to reproduce/verify) | VERIFIED / UNVERIFIED / INFERRED |

### Categories

- **Secrets**: tokens, keys, credentials in tracked or accessible locations.
- **Runtime**: process model, singleton constraints, restart behavior.
- **Artifacts**: event streams, logs, decision records — format, integrity, access.
- **Deployment**: service configuration, user model, update process.
- **Network**: exposed ports, TLS configuration, API endpoints.
- **Configuration**: drift risk, env-var-controlled behavior, safety mechanism flags.

---

## Usage rules

1. **Every claim must cite a specific artifact.** File path and line number, command and output, or configuration key and value. Claims without evidence are marked INFERRED.
2. **INFERRED claims cannot be used as basis for guard design.** They indicate areas requiring further investigation.
3. **VERIFIED means reproducible.** Another person (or agent) following the evidence source must be able to independently confirm the claim.
4. **UNVERIFIED means evidence exists but has not been independently confirmed.** Typical for observations from live systems that require host access to re-check.

---

## What counts as verified

- Direct evidence from source code (file, line, function — confirmed by reading).
- Direct evidence from configuration (config key, value — confirmed by reading).
- Direct evidence from live system output (command output captured and timestamped).
- Direct evidence from version control (commit hash, diff).

## What does NOT count as verified

- Interpretation or assumption ("it probably works this way").
- Inference from absence ("there is no firewall config, so the firewall is off").
- Second-hand reporting ("someone said the token was rotated").
- Outdated evidence (verified once but not re-checked after system changes).

---

## Observations

| ID | Category | Claim | Evidence source | Verification method | Status |
|----|----------|-------|-----------------|---------------------|--------|
| | | (populate when analyzing a specific protected system) | | | |

---

## Next steps

After populating this table for a specific protected system:

1. Move VERIFIED observations to [VERIFIED_FACTS.md](VERIFIED_FACTS.md).
2. Use verified facts to populate [THREAT_MODEL_DRAFT.md](THREAT_MODEL_DRAFT.md).
3. Record unresolved gaps in [OPEN_QUESTIONS.md](OPEN_QUESTIONS.md).
