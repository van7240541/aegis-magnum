# NON-CANONICAL DRAFT

# VERIFIED_FACTS — Evidence Registry

Status: **NON-CANONICAL DRAFT**
Purpose: Strict evidence registry containing only facts that passed the verification gate. Facts here are verified claims but do not have architectural authority until referenced by a CANONICAL document.

---

## Status rule

Facts in this document are verified observations — they describe what exists in a specific protected system. They are NOT invariants, rules, or contracts. A fact becomes architecturally relevant only when a canonical document (invariant, boundary rule, adapter spec) references it as basis for a guard rule.

---

## Structure

| ID | Claim | Evidence (file:line or command output) | Verification date | Protected system | Status |
|----|-------|----------------------------------------|--------------------|------------------|--------|
| F-001 | (example: "API token is present in git-tracked config file") | (example: "config.yaml:10") | (YYYY-MM-DD) | (system name) | VERIFIED |

---

## Usage rules

1. **No fact may be added without exact evidence.** "It seems like..." or "based on my understanding..." are not facts.
2. **No fact may be promoted to a canonical invariant without separate review.** Promotion requires creating or updating a canonical document that explicitly cites the fact ID.
3. **Facts are system-specific.** Each fact belongs to a specific protected system (identified in the table). Guard-universal facts do not belong here — they belong in canonical invariants.
4. **Facts may become stale.** If the protected system changes, previously verified facts must be re-verified. Stale facts should be marked with a note and date.

---

## Separation from reconnaissance

- [SECURITY_RECONNAISSANCE.md](SECURITY_RECONNAISSANCE.md) records all observations (verified, unverified, inferred).
- This document records **only** those that survived the verification gate.
- An observation moves here when it has exact evidence and has been independently confirmed.

---

## Facts

| ID | Claim | Evidence | Verification date | Protected system | Status |
|----|-------|----------|-------------------|------------------|--------|
| | | (populate when verifying observations for a specific protected system) | | | |
