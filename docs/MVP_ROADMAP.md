# CANONICAL SOURCE

# MVP_ROADMAP — Implementation plan

**Purpose:** Staged path from **security canon** (this export) to optional **guard code**, without acquiring decision authority. **No stage** implements domain-specific execution or unvalidated execution-request submission.

---

## Stage 0 — Security contour operationalized (parallel to any code)

**Goal:** The project’s **chain of trust** is real, not only paper.

Deliverables (organizational / ops, not Aegis code):

- Secret **inventory** and verification that no credentials live in git — [SECRETS_AND_KEY_MANAGEMENT.v1.md](SECRETS_AND_KEY_MANAGEMENT.v1.md).
- **SSH**, **firewall**, **patching**, **logging** baseline applied per [SERVER_HARDENING_BASELINE.v1.md](SERVER_HARDENING_BASELINE.v1.md).
- **IR playbook** understood — [INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md](INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md).
- **Alignment** read with host product — [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md).

**No guard process required** for Stage 0 completion.

---

## Stage 1 — Minimal sentinel (OBSERVE-first)

**Goal:** A running guard that **observes** and emits **structured audit events** only.

Deliverables (illustrative names):

- Orchestrator shell, **OBSERVE** mode only.
- Process / artifact / config drift checks as read-only.
- Guard-local **audit sink** (append-only, reviewable).
- One alert channel optional — if present, must not imply execution authority.
- Generic adapter stub per [docs/ADAPTER_CONTRACT.v1.md](docs/ADAPTER_CONTRACT.v1.md) (draft).

**Explicitly out of scope:** VERIFY/ALERT/QUARANTINE in the same deliverable unless separately approved; no quarantine bridge; no BLOCK — [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md).

Success criteria: see [COLLABORATOR_HANDOFF.md](../COLLABORATOR_HANDOFF.md) §10.

---

## Stage 2 — VERIFY + ALERT

**Goal:** Adapter-defined **invariants** and operator notifications; still no execution.

Deliverables:

- Policy evaluation against adapter invariants.
- VERIFY mode; structured failure reporting.
- **Independent** alert identity vs. operational bots where possible.

---

## Stage 3 — Quarantine request path (optional)

**Goal:** **Request** boundary restriction only through mechanisms the **protected system** owns.

Deliverables:

- Quarantine **request** formatter; full audit of request lifecycle on guard side.
- Protected system remains authoritative on whether to act.

---

## Stage 4 — Deeper integrity

**Goal:** Stronger tamper and integrity signals (hashes, chains) where the protected system supports them.

---

## Stage 5 — Future execution boundary (host product + separate contract)

**Goal:** Only if the protected system introduces external execution: **separate** versioned enforcement contract — not part of this export’s v1 scope. Principles: [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md).

---

## Deployment note

**Phase A:** Guard on same host as protected system, **separate user**. **Phase B:** Guard on separate host — stronger isolation, more integration work. Design Stage 1–3 so Phase B does not require core rewrite.

---

## Priorities

1. **Stage 0** is not optional for a serious deployment.
2. **Stage 1** must pass OBSERVE success criteria before expanding modes.
3. **Execution** is not a milestone here — containment is documented only until product-specific contracts exist.

---

**Version:** v1
