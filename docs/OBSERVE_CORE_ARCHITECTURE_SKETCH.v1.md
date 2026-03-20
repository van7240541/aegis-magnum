# CANONICAL SOURCE

# OBSERVE_CORE_ARCHITECTURE_SKETCH v1

**Purpose:** **Documentation-only** sketch of the first code deliverable (OBSERVE-only). No implementation here — prevents implementers from collapsing layers. See [COLLABORATOR_HANDOFF.md](../COLLABORATOR_HANDOFF.md) §10 and [MVP_ROADMAP.md](MVP_ROADMAP.md) Stage 1.

---

## Components (conceptual)

| Piece | Responsibility | Authority |
|-------|------------------|-----------|
| **Orchestrator** | Schedule observation cycles; mode = OBSERVE only | None over host |
| **Adapter (read path)** | Resolve artifact paths; read-only I/O; emit normalized records | Structural mapping only — [ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md) |
| **Audit sink** | Append-only guard-local log (format TBD in code) | Guard-owned only |
| **Config** | Paths, cadence, adapter id — **no** secrets in repo | Operators supply secrets via env / secret store |

**Explicitly absent in first deliverable:** VERIFY escalation, ALERT channels (unless separately approved), QUARANTINE, BLOCK, execution hooks, writes to host artifacts.

---

## Data flow (observe-only)

```text
Protected system artifacts (read-only) ──► Adapter ──► Normalized observe records ──► Audit sink
                                                                              │
                                                                              └──► (optional later: alert — not v1 first deliverable unless scoped)
```

No backward edge to the protected system.

---

## Disable switch

Process must be stoppable; host must behave identically with guard **off** (aside from normal read I/O if co-located).

---

## Success gate

Per [COLLABORATOR_HANDOFF.md](../COLLABORATOR_HANDOFF.md): reproducible audit artifact; zero behavior change; full disable; one valid non-vacuous observe signal.

---

**Version:** v1
