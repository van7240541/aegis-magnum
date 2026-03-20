# CANONICAL SOURCE

# PROJECT_DISCIPLINE v1 — Operational Law

Status: **CANON**
Scope: All participants (human, AI agent, automated system) operating within Aegis Magnum.

---

## 1. Purpose

This document defines the foundational operating rules of the Aegis Magnum project. Every change, every decision, and every agent action is subject to this discipline. Violation invalidates architectural integrity.

---

## 2. Canon-first

- The only source of truth is the canonical documentation in this repository.
- No chat transcript, no agent output, no verbal agreement is authoritative.
- If a claim is not grounded in a canonical document, it is not binding.
- When code and canon conflict, canon wins. The conflict must be resolved explicitly.

---

## 3. Fail-closed

- Under any uncertainty, the default outcome is **NO ACTION / HOLD**.
- If a guard module cannot determine its operating state, it must refuse to act.
- If inputs are missing, ambiguous, or contradictory, the outcome is prohibition, not allowance.
- "Probably safe" is not a valid basis for action.

---

## 4. No hidden authority

- Every source of authority must be traceable to a canonical contract.
- No module, agent, or process may acquire enforcement capability without explicit authorization in a versioned document.
- Silent authority expansion (gaining power without a contract update) is a discipline violation.
- Observation does not imply authority. A module that reads data does not thereby gain the right to act on it.

---

## 5. Detection and enforcement are separate

- Detection (observe, verify, alert) is always permitted within the read path defined by contracts.
- Enforcement (quarantine, block) requires explicit mode authorization per [MODE_CONTRACT.v1.md](MODE_CONTRACT.v1.md).
- A module that detects a problem must not automatically enforce a remedy unless its current mode and contract permit it.

---

## 6. Document precedence

When documents conflict, the following precedence applies (highest first):

1. `SECURITY_INVARIANTS.v1.md` — non-negotiable invariants
2. `SECURITY_BOUNDARY.v1.md` — what the guard may and may not do
3. `MODE_CONTRACT.v1.md` — mode definitions and transitions
4. `QUARANTINE_CONTRACT.v1.md` — quarantine semantics
5. `AUTHORITY_BOUNDARY.v1.md` — zone permissions and prohibitions
6. `PROJECT_DISCIPLINE.v1.md` — this document (operational rules)
7. `ADAPTER_CONTRACT.v1.md` — adapter interface
8. All other canonical documents

If a lower-precedence document grants authority that a higher-precedence document restricts, the restriction wins.

---

## 7. Change rules

- Every change must have explicit scope (which files, which sections, which behavior).
- Every change must describe a rollback path.
- No change may expand authority without updating the relevant contract.
- Changes to canonical documents require a version bump when semantics change.
- Drift (undocumented deviation from canon) is a discipline violation.

---

## 8. Uncertainty protocol

When a participant encounters a situation not covered by existing canon:

1. Stop. Do not invent a resolution.
2. Record the gap in [OPEN_QUESTIONS.md](OPEN_QUESTIONS.md).
3. Do not proceed past the ambiguity until it is resolved by an authorized decision.
4. Default to the most restrictive interpretation available.

---

## 9. AI agent rules

AI agents operating in this repository must:

- Not invent missing definitions.
- Not expand authority without an explicit contract.
- Not mix detection and enforcement in the same action.
- Not write code before the governance frame exists.
- Stop when documents conflict and report the conflict.
- Not continue reasoning when canonical basis is absent.
- Treat any active measure as forbidden unless a contract explicitly permits it.

---

## Change control

Any change that weakens fail-closed, removes authority traceability, or allows implicit permission requires a version bump of this document and alignment with SECURITY_INVARIANTS and SECURITY_BOUNDARY.
