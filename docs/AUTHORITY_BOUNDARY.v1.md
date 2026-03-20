# CANONICAL SOURCE

# AUTHORITY_BOUNDARY v1

Status: **CANON**
Scope: Defines what the guard system may do in each operational zone and what it must never do. Separates observation from influence.

---

## 1. Core principle

The guard system operates **outside** the protected system's decision boundary. It may observe, verify, and alert. It may request quarantine. It must never silently influence the protected system's decisions, permissions, or execution.

---

## 2. Zones

### Zone: OBSERVE

The guard may:
- Read the protected system's artifacts (logs, event streams, configuration fingerprints)
- Read process metadata (PID, liveness, command line)
- Read service status (via the host's service manager, read-only)
- Read version control state (commit hash, branch, drift status)

The guard must not:
- Modify any file it reads
- Interpret observed data as authorization to act (observation is not authority)

### Zone: VERIFY

The guard may:
- Compute checks against observed data (schema validation, integrity checks, invariant conformance)
- Score system health internally
- Compare current state against known baselines

The guard must not:
- Communicate verification results to the protected system in a way that alters its behavior
- Treat a failed check as automatic authorization for enforcement

### Zone: ALERT

The guard may:
- Notify operators via independent channels (separate from the protected system's own alerting)
- Log alert events in the guard's own audit trail
- Escalate alert severity based on policy

The guard must not:
- Use alerting as a side channel to trigger automated enforcement in the protected system
- Alert through the protected system's own notification identity (to prevent single-channel compromise)

### Zone: QUARANTINE

The guard may:
- Submit a quarantine request to the protected system's operator/emergency mechanism as defined by the adapter
- Only when operating in QUARANTINE mode per [MODE_CONTRACT.v1.md](MODE_CONTRACT.v1.md)
- Only with full audit trail per [QUARANTINE_CONTRACT.v1.md](QUARANTINE_CONTRACT.v1.md)

The guard must not:
- Execute quarantine without being in QUARANTINE mode
- Modify the protected system's internal state directly
- Treat quarantine as a command (it is a request)

### Zone: ENFORCE (forbidden in v1)

The guard must not:
- Interpose on the protected system's execution path
- Drop, rewrite, or hold the protected system's outbound actions
- Act as a gate between the protected system and external services

This zone requires a separate `ENFORCEMENT_CONTRACT` that does not yet exist.

---

## 3. Explicit prohibition of silent influence

The guard must not influence the protected system through any mechanism not listed in this document. This includes but is not limited to:

- Writing to the protected system's configuration files
- Setting environment variables for the protected system's processes
- Modifying the protected system's source code or runtime scripts
- Injecting events into the protected system's artifact stream
- Altering the protected system's network configuration or firewall rules
- Signaling the protected system's processes (kill, HUP, etc.) except through the defined quarantine mechanism

If an influence path exists that is not covered by a contract, it is forbidden by default.

---

## 4. Where the guard ends

The guard's authority boundary is defined by:

- Its own canonical documents (this repository)
- The adapter contract for the specific protected system
- The current operating mode

Beyond this boundary, the guard has no rights. The protected system's own decision authority, permission logic, and execution control remain exclusively with the protected system.

---

## Change control

Expanding the guard's authority into new zones requires a new version of this document and a corresponding contract for the new zone.
