# CANONICAL SOURCE

# SYSTEM_IDENTITY — Aegis Magnum

Status: **CANON**
Purpose: Define what this project is, what it is not, where it sits in architecture, and who owns authority.

---

## What is Aegis Magnum

Aegis Magnum is a guard architecture framework. It observes, verifies, and alerts on the health and integrity of a protected system. When explicitly authorized, it may request quarantine at the boundary.

It is designed to be:

- **Universal**: the core is domain-agnostic; project-specific logic lives in adapters.
- **Discipline-first**: governance documents exist before code; canon is the source of truth.
- **Non-intrusive**: the guard attaches to a protected system from outside, without becoming part of its decision authority.

---

## What Aegis Magnum is NOT

- It is not a decision system. It does not interpret domain data, compute risk, or grant permissions.
- It is not a second execution layer. It does not place orders, submit transactions, or trigger actions in the protected system.
- It is not a runtime module. It does not run inside the protected system's process or share its memory space.
- It is not a replacement for the protected system's own safety mechanisms. It complements them from outside.
- It is not an autonomous agent. It does not act without explicit authorization from canonical contracts.

---

## Where it sits in architecture

```
Protected System (owns all decision authority)
    |
    | emits artifacts, logs, process state
    v
Aegis Magnum (observes, verifies, alerts)
    |
    | via adapter
    v
Project-specific invariants and quarantine mechanism
    |
    | produces
    v
Alerts / evidence / quarantine requests
```

The guard sits outside the protected system's trust boundary. It reads the protected system's outputs but does not write to its inputs.

---

## Who owns authority

The protected system owns all decision authority. Always.

Aegis Magnum does not own, share, or borrow decision authority. Its only write capability is the quarantine request, which goes through the protected system's own operator/emergency mechanism as defined by the adapter.

If the adapter does not define a quarantine mechanism, the guard has zero write capability for that protected system.

---

## Integration model

Aegis Magnum connects to protected systems via **adapters**:

- Each adapter implements the interface defined in [ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md).
- The adapter tells the guard where to look, what to check, and how to quarantine.
- Multiple adapters can coexist (one per protected system).
- The core never imports or executes protected system code.

---

## Core principle

> The guard protects the boundary, not the decision.
> It enforces integrity, not authority.
