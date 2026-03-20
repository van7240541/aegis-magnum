# CANONICAL SOURCE

# QUARANTINE_CONTRACT v1

Status: **CANON**
Scope: Defines the strict semantics of quarantine — the only enforcement action available to the guard in v1.

---

## 1. Definition

Quarantine is a **boundary restriction request** directed at the protected system's existing operator/emergency mechanism.

Quarantine is **not** a command. It is a request that the protected system's operator gate evaluates. The guard does not control whether or how the protected system acts on the request.

---

## 2. Hard prohibitions

Quarantine MUST NEVER:

- Modify the protected system's decision logic, permission verdicts, risk computation, or eligibility semantics.
- Write to, edit, or forge entries in the protected system's runtime artifacts (logs, event streams, decision records).
- Alter the protected system's configuration, environment variables, or source code.
- Bypass the protected system's own operator/emergency mechanism (the quarantine path is defined by the adapter, not invented by the guard).
- Silently re-apply on a timer without operator visibility. If quarantine is sustained, the guard must alert on both initial application and continued lock state.
- Act as a substitute for human operator judgment. Quarantine buys time; it does not resolve incidents.

---

## 3. Required fields

Every quarantine request must include:

| Field | Description |
|-------|-------------|
| `reason` | Non-empty string explaining the trigger condition |
| `ts_ms` | Timestamp of the quarantine request (milliseconds or ISO 8601) |
| `origin` | Identity of the requesting entity (e.g. `guard:<service_name>`, `human`) |
| `invariant_id` | Which invariant violation triggered this (if applicable; may be `null` for manual quarantine) |
| `evidence` | Reference to the detection that caused the request (file, line, check ID) |

The adapter translates these fields into the payload format expected by the protected system's quarantine mechanism.

---

## 4. Preconditions

Quarantine may only be requested when:

1. The guard is operating in **QUARANTINE** mode per [MODE_CONTRACT.v1.md](MODE_CONTRACT.v1.md).
2. The adapter declares quarantine capability as available (see [ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md) section 2.6).
3. A detection event has occurred that justifies the request (the guard must not quarantine preemptively without evidence).

If any precondition is not met, the guard must fall back to ALERT.

---

## 5. Removal

- Quarantine removal must be **explicit**. There is no automatic timeout or self-clearing.
- Removal must be performed by an authorized principal (human operator or explicitly authorized automated process).
- Removal must be logged in the guard's own audit trail with: who removed, when, and why.
- The guard must alert when quarantine is removed, with the same visibility as the original quarantine alert.

---

## 6. Audit trail

Every quarantine lifecycle event must be recorded in the guard's own audit log (not in the protected system's artifacts):

- Quarantine requested (with all required fields)
- Quarantine confirmed (if the protected system acknowledges)
- Quarantine sustained (periodic heartbeat while lock is active)
- Quarantine removed (with removal details)

---

## 7. Scope limitation

Quarantine protects the boundary. It does not:

- Fix the underlying problem
- Diagnose root cause
- Modify the protected system's internal state
- Replace incident response

After quarantine, the incident must be investigated and resolved by human operators or an authorized process.

---

## 8. Future provisions

- Cryptographic signing of quarantine requests is optional in v1. If added, it must be specified in a version bump of this document.
- Multi-system quarantine coordination (quarantining multiple protected systems simultaneously) is out of scope for v1.

---

## Change control

Expanding quarantine capabilities (new mechanisms, new payload fields, automated removal) requires a version bump of this document.
