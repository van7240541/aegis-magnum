# CANONICAL SOURCE

# MAIN_LINE_PROJECT_INSTRUCTION v1

**Purpose:** Paste-friendly **project / chat instruction** for “Aegis Magnum — Main Line.” It **summarizes** this repository; it does **not** replace the other canon files.

**Binding text** for edge cases: [README.md](../README.md), [COLLABORATOR_HANDOFF.md](../COLLABORATOR_HANDOFF.md), [SYSTEM_SECURITY_MODEL.v1.md](SYSTEM_SECURITY_MODEL.v1.md), [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md), [ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md).

---

## Instruction block (copy below this line)

```
AEGIS MAGNUM — MAIN LINE (v1) — PROJECT INSTRUCTION

SCOPE OF THIS PROJECT
- Coordinate architecture and priorities for Aegis Magnum.
- Guard rules below apply to guard/adapters/boundary discussions.
- This repo also defines SECURITY CONTOUR (trust chain, secrets, host hardening, IR). For ops/infra/secrets/IR questions, use SYSTEM_SECURITY_MODEL + SECRETS_AND_KEY_MANAGEMENT + SERVER_HARDENING_BASELINE + INCIDENT_RESPONSE_AND_KEY_COMPROMISE — do not answer from guard-only rules alone.

SYSTEM ROLE (GUARD)
Aegis is a security and boundary guard framework. NOT: decision engine, execution system, strategy/domain layer. IS: observation, structural verification, boundary integrity, audit/alert, and REQUEST for restriction (quarantine) via host-owned, contract-defined mechanisms.

PRIMARY FUNCTION
Observe protected-system behavior; verify STRUCTURAL/integrity constraints and, where contracted, mechanical consistency of host-stated policy outputs with the host’s published canon; emit audit/alert; REQUEST quarantine. Do NOT decide, execute, optimize, or interpret domain merit or “good/bad” outcomes.

CORE PRINCIPLES
- Guard protects the BOUNDARY, not the DECISION.
- Compute ≠ authority: read/compute/analyze do not grant control or permission.
- Zero decision authority; zero execution authority for Aegis.
- Protected system owns decision authority. Boundary validation for external action is owned by the HOST; Aegis does not replace host policy engines.

NON-DEPENDENCY
Protected system must run correctly without Aegis. Critical-path dependency on Aegis = invalid design.

BASELINE
Observe → structural verify → report. No enforcement unless explicit, contract-bound, externally owned. Quarantine = request only; no unilateral block or mutation of protected runtime truth.

ADAPTERS
Only interface to hosts. MAY map/validate STRUCTURE. MUST NOT: domain evaluation, scoring/ranking, decision logic, merit/correctness of outputs. Host vocabulary in adapter config, not universal canon.

FUTURE EXECUTION (v1)
Not implemented. Conceptual universal high-risk class only. Do not simulate execution or smuggle execution design into universal core.

PROHIBITIONS
No hidden authority; no merging guard with decision path; no embedding in execution flow; no mutating protected artifacts; no implicit enforcement; no substituting host validation layers. Violation = architectural breach.

WHEN UNCERTAIN
Default NO expansion of authority. DOCUMENT ambiguity (tracker / ADAPTER_RESEARCH), then align with SYSTEM_SECURITY_MODEL, SECURITY_BOUNDARY_ALIGNMENT, FUTURE_EXECUTION_SECURITY before implementing.

THIS CHAT IS NOT FOR
Detailed adapter implementation code, deep threat-model execution, runtime coding — route to subprojects/repo.

SOURCE OF TRUTH
Git files in this repository; this block summarizes only.

FINAL LAW
Aegis protects by remaining outside decision and execution authority. If Aegis becomes required, embedded in the critical path, or decision-influencing, the design has failed.
```

---

**Version:** v1
