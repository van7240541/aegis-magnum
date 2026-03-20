# CANONICAL SOURCE

# MODE_CONTRACT v1

Status: **CANON**
Scope: Defines the operating modes of the guard system, their semantics, and allowed transitions. This document covers ONLY mode definitions — it does not define what the guard may observe or verify (see [SECURITY_BOUNDARY.v1.md](SECURITY_BOUNDARY.v1.md)) or the quarantine mechanism (see [QUARANTINE_CONTRACT.v1.md](QUARANTINE_CONTRACT.v1.md)).

---

## 1. Mode definitions

### OBSERVE (default)

- **Purpose**: Read-only telemetry. The guard collects data and maintains internal state.
- **Allowed**: Read artifacts, read process metadata, read service status, read version control state.
- **Forbidden**: Any outbound action (no alerts, no quarantine, no writes).
- **When to use**: Baseline data collection, initial deployment, passive monitoring.

### VERIFY

- **Purpose**: Active checking. The guard runs invariant checks and scores system health.
- **Allowed**: Everything in OBSERVE, plus compute checks against observed data, compare against baselines, maintain internal health scores.
- **Forbidden**: Any outbound action (no alerts, no quarantine, no writes).
- **When to use**: After OBSERVE has established a baseline; validation-only runs.

### ALERT

- **Purpose**: Operational notifications. The guard emits alerts to operators when checks fail.
- **Allowed**: Everything in VERIFY, plus emit alerts via configured channels (Telegram, webhook, email, stdout).
- **Forbidden**: Quarantine requests, any write to the protected system's state, any enforcement action.
- **When to use**: Normal operational monitoring.

### QUARANTINE

- **Purpose**: Boundary restriction request. The guard may request the protected system to self-restrict via its operator/emergency mechanism.
- **Allowed**: Everything in ALERT, plus submit quarantine requests per [QUARANTINE_CONTRACT.v1.md](QUARANTINE_CONTRACT.v1.md).
- **Forbidden**: Direct modification of the protected system's state, code, config, or artifacts. The quarantine request goes through the adapter-defined mechanism only.
- **When to use**: Critical invariant violations that require immediate boundary protection.

### BLOCK (not available in v1)

- **Purpose**: Interpose on the protected system's execution path (drop, rewrite, or hold outbound actions).
- **Status**: Forbidden until a separate `ENFORCEMENT_CONTRACT` exists. No implementation, no configuration, no partial activation.
- **When available**: Only after a versioned enforcement contract is created, reviewed, and linked from this document.

---

## 2. Default mode

On startup, after restart, or when mode state is unknown, the guard must operate in **OBSERVE**.

If the guard cannot determine its current mode, it must fall back to OBSERVE (fail-closed: least authority).

---

## 3. Allowed transitions

```
OBSERVE --> VERIFY --> ALERT --> QUARANTINE
                                     |
QUARANTINE --> ALERT (de-escalation)  |
ALERT --> VERIFY (de-escalation)      |
VERIFY --> OBSERVE (de-escalation)    |
                                     |
BLOCK: not reachable in v1 ----------+
```

Transitions must be:
- Explicit (triggered by configuration or operator command, not implicit)
- Logged (every transition produces an audit record with timestamp, origin, reason)
- Reversible (de-escalation is always permitted)

Skipping modes during escalation is permitted (e.g. OBSERVE directly to ALERT) if the configuration or operator command explicitly requests it.

---

## 4. Forbidden transitions

- Any transition to BLOCK is forbidden in v1.
- No mode may be activated without the corresponding contract being present and valid:
  - QUARANTINE requires [QUARANTINE_CONTRACT.v1.md](QUARANTINE_CONTRACT.v1.md)
  - BLOCK requires a future ENFORCEMENT_CONTRACT (does not exist)

---

## 5. Mode logging

Every mode change must produce an audit record containing:

- `ts_ms` — timestamp of the transition
- `from_mode` — previous mode
- `to_mode` — new mode
- `origin` — who or what triggered the transition (operator, config, policy, auto-escalation)
- `reason` — why the transition occurred

Mode records are written to the guard's own audit trail, not to the protected system's artifacts.

---

## Change control

Adding new modes or enabling BLOCK requires a version bump of this document and creation of the corresponding contract.
