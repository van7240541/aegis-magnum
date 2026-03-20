# NON-CANONICAL DRAFT

# OPEN_QUESTIONS — Architecture Blockers

Status: **NON-CANONICAL DRAFT**
Purpose: Track must-resolve questions that block architecture approval, implementation decisions, or guard activation. Questions here indicate gaps in knowledge.

---

## Status rule

Open questions are blockers. No architecture decision may be made while a relevant OPEN question remains unresolved. This document does not grant or restrict authority — it records what we do not yet know.

---

## Structure

| ID | Question | Why it matters (what breaks if wrong) | How to resolve | Resolution status |
|----|----------|---------------------------------------|----------------|-------------------|
| OQ-001 | (example) | (example) | (example) | OPEN / RESOLVED / DEFERRED |

### Resolution status

- **OPEN**: Not yet answered. Blocks any decision that depends on the answer.
- **RESOLVED**: Answered with evidence. Must cite the resolution evidence (fact ID, document, or decision record).
- **DEFERRED**: Intentionally postponed. Must state why deferral is safe (i.e., what assumption is being made and what happens if it is wrong).

---

## Usage rules

1. **OPEN questions block dependent decisions.** If a guard invariant, adapter design, or mode configuration depends on an unanswered question, it must wait.
2. **RESOLVED questions must cite evidence.** A resolution without evidence is an opinion, not a resolution.
3. **DEFERRED questions must state the safety assumption.** "We'll figure it out later" is not a valid deferral reason. Valid: "We defer because the risk only materializes when execution goes live, and execution is currently inactive."
4. **Questions can originate from any source**: reconnaissance, threat model, implementation review, or external input.
5. **Questions are never deleted.** Resolved questions stay in the table with their resolution for audit trail.

---

## Questions

| ID | Question | Why it matters | How to resolve | Resolution status |
|----|----------|----------------|----------------|-------------------|
| | | (populate when analyzing a specific protected system or making architecture decisions) | | |
