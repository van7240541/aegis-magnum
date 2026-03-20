# CANONICAL SOURCE

# ADAPTER_CONTRACT v1

Status: **CANON**
Scope: Defines the interface that every project-specific adapter must implement to connect the guard system to a protected system.

---

## 1. Purpose

The guard core is domain-agnostic. It does not know what the protected system does, what its artifacts look like, or how to quarantine it.

The adapter bridges this gap. It provides the guard core with:

- Where to look (artifact sources, process identity, configuration paths)
- What to check (invariants specific to the protected system)
- How to quarantine (the protected system's operator/emergency mechanism)

---

## 2. Required adapter interface

Every adapter must implement the following capabilities. The exact API shape (classes, functions, config files) is an implementation decision; the capabilities are mandatory.

### 2.1 Discovery

Provide the guard with a description of the protected system:

- System name and version
- Expected runtime processes (command line patterns, PID file locations)
- Expected service units (if applicable)
- Repository location (for drift detection)

### 2.2 Artifact sources

List the protected system's artifact files that the guard should monitor:

- File paths (absolute or relative to a configured root)
- Expected format (JSONL, plain text, binary)
- Expected schema (field names, required fields) where applicable
- Growth expectation (append-only, rotated, replaced)

### 2.3 Critical files

List files whose modification should trigger alerts:

- Configuration files
- Service unit files
- Entrypoint scripts
- Any file whose change could alter the protected system's behavior

For each: whether to track content hash, modification time, or both.

### 2.4 Invariants

Define the protected system's security invariants that the guard should verify:

- Invariant ID (e.g. `SI-1`)
- Description
- Verification method (what to check, how to check it)
- Severity on failure (WARNING, CRITICAL)
- Reference to the protected system's canonical documentation (if applicable)

### 2.5 Process specification

Define the expected runtime process:

- Expected command line (pattern or exact match)
- Expected user/group
- Singleton constraint (lock file path, if applicable)
- Health indicators (artifact growth, heartbeat file, expected log patterns)

### 2.6 Quarantine capabilities

Define how the guard may request quarantine:

- Mechanism type (file write, API call, signal, or other)
- Target path or endpoint
- Required payload fields (per [QUARANTINE_CONTRACT.v1.md](QUARANTINE_CONTRACT.v1.md))
- Confirmation method (how to verify the quarantine was received)
- Removal method (how quarantine is lifted)

If the protected system has no quarantine mechanism, the adapter must declare `quarantine: not_available` and the guard must not operate in QUARANTINE mode for that system.

---

## 3. Adapter prohibitions

An adapter must not:

- Contain decision logic for the protected system
- Import or execute the protected system's runtime code
- Write to the protected system's artifacts (except through the defined quarantine mechanism)
- Hardcode secrets (all credentials via environment or secret manager)
- Bypass the guard core's mode restrictions

---

## 4. Adapter versioning

Each adapter carries its own version, independent of the guard core version. Version bumps are required when:

- Artifact schemas change in the protected system
- Invariant definitions change
- The quarantine mechanism changes
- The process specification changes

---

## 5. Generic fallback

If no adapter exists for a given protected system, the guard core may operate with a minimal generic adapter that provides:

- File monitoring (paths configured externally)
- Process monitoring (command line pattern configured externally)
- No invariant checking (no system-specific knowledge)
- No quarantine capability

This allows basic OBSERVE + VERIFY + ALERT for any system, with system-specific intelligence added via custom adapters.

---

## Change control

Changes to the required interface (adding or removing required capabilities) require a version bump of this document.
