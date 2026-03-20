# EXPORT BOOTSTRAP

# MVP_ROADMAP — Implementation Plan

Status: **EXPORT BOOTSTRAP**
Purpose: Define the staged implementation plan for Aegis Magnum from governance skeleton to operational guard.

---

## Stage 1 — Minimal Sentinel

**Goal**: A running guard that can observe a protected system and alert on basic health failures.

Deliverables:
- `engine.py` — main orchestrator
- `modes.py` — OBSERVE mode only
- `process_monitor.py` — check process liveness (PID, lock file, command line)
- `integrity.py` — file size monotonicity (artifact growth detection)
- `config_monitor.py` — configuration fingerprint baseline and drift detection
- `audit_logger.py` — guard's own event log
- One alert channel (Telegram or stdout)
- Generic JSONL adapter (configurable paths, no system-specific invariants)
- Basic configuration (`aegis.example.yaml`)

**Mode**: OBSERVE + basic ALERT (process down, artifact stale, config drift).

**No quarantine. No invariant verification beyond file health.**

---

## Stage 2 — Adapter invariants

**Goal**: Add system-specific invariant checking via the adapter interface.

Deliverables:
- `policy_engine.py` — evaluate adapter-provided invariants against observed data
- `invariants.py` — InvariantResult model
- `event_reader.py` — JSONL tail with offset tracking
- VERIFY mode activation
- First project-specific adapter (artifact schemas, join keys, invariant definitions)
- Secret scanning (detect credential patterns in tracked files)

**Mode**: OBSERVE + VERIFY + ALERT.

**Invariants checked**: adapter-defined (e.g., fail-closed evaluation, artifact append-only, no secrets in source).

---

## Stage 3 — Quarantine bridge

**Goal**: Enable boundary restriction requests through the adapter-defined mechanism.

Deliverables:
- `quarantine.py` — quarantine request handler with precondition checks
- QUARANTINE mode activation
- Adapter quarantine capability (mechanism, payload, confirmation, removal)
- Quarantine audit trail (request, confirm, sustain, remove)
- Alert on quarantine lifecycle events

**Mode**: Full OBSERVE + VERIFY + ALERT + QUARANTINE.

**Quarantine is advisory only. The protected system decides whether to act on it.**

---

## Stage 4 — Artifact integrity

**Goal**: Add cryptographic integrity checking for protected system artifacts.

Deliverables:
- Hash snapshot comparison (periodic file hashes stored by the guard)
- Hash chain verification (when the protected system supports it)
- Tamper detection alerts (shrinkage, truncation, hash mismatch)
- Integrity ledger (guard's own record of artifact state over time)

**Depends on**: protected system supporting or adopting hash chain in its artifacts.

---

## Stage 5 — Execution boundary guard (future)

**Goal**: If and when a protected system has a live execution path (intent to external action), provide optional interposition.

Deliverables:
- ENFORCEMENT_CONTRACT (new canonical document)
- BLOCK mode specification
- Interposition module (between intent and execution, reject-only, never modify)
- Hard caps (size, frequency, allowed targets)
- Fail-closed: no execution without guard confirmation

**This stage requires a separate canonical contract. It is not part of v1 scope.**

---

## Priorities

- Stages 1-3 form the MVP. They provide observation, verification, alerting, and boundary quarantine.
- Stage 4 adds depth (cryptographic integrity) but is not required for initial deployment.
- Stage 5 is future work that depends on the protected system's execution layer going live.

---

## Deployment model

**Phase A (recommended start)**: Guard runs on the same host as the protected system, under a separate user account. Simpler to deploy, shared failure domain.

**Phase B (future)**: Guard runs on a separate host. True external monitoring. Requires remote artifact access (rsync, API, or log shipping). Better isolation but more complex.

Design for Phase A, architect so that Phase B requires no core rewrite.
