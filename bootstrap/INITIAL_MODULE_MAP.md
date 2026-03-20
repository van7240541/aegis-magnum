# EXPORT BOOTSTRAP

# INITIAL_MODULE_MAP — Module Inventory

Status: **EXPORT BOOTSTRAP**
Purpose: Map each planned module with its purpose, authority level, and dependencies.

---

## Core modules

| Module | Purpose | Authority | Dependencies |
|--------|---------|-----------|--------------|
| `engine.py` | Main orchestrator: config loading, adapter init, monitor dispatch, event routing | None (coordination only) | modes, scheduler, adapter, audit_logger |
| `modes.py` | Mode state machine: current mode, transitions, validation, fail-closed default | None (state tracking only) | audit_logger |
| `scheduler.py` | Tick-based or event-driven scheduling for monitor execution | None (timing only) | engine |
| `event_reader.py` | Read protected system artifacts: tail JSONL, offset tracking, no duplication, restart recovery | Read-only (observation) | adapter (for file paths) |
| `policy_engine.py` | Evaluate invariants against observed data; produce InvariantResult records | Read-only (verification) | invariants, adapter |
| `invariants.py` | Base invariant model: InvariantResult (id, severity, status, reason, evidence) | None (data model) | — |
| `integrity.py` | File integrity monitoring: size monotonicity, hash snapshots, truncation detection | Read-only (verification) | adapter (for critical files) |
| `process_monitor.py` | Process liveness: PID check, lock file validation, command line match, service status | Read-only (observation) | adapter (for process spec) |
| `config_monitor.py` | Configuration drift detection: hash baseline, mtime tracking, drift alerts | Read-only (observation) | adapter (for config paths) |
| `quarantine.py` | Quarantine request handler: validate preconditions, delegate to adapter mechanism, log lifecycle | Write (quarantine request only) | adapter, modes, audit_logger |
| `audit_logger.py` | Guard's own audit trail: mode changes, alerts, quarantine events, invariant results | Write (guard's own log only) | — |

---

## Adapter layer

| Module | Purpose | Authority |
|--------|---------|-----------|
| `adapters/base.py` | Abstract interface per ADAPTER_CONTRACT.v1.md | None (interface) |
| `adapters/generic_jsonl/adapter.py` | Generic file-based adapter: configurable paths, basic schema, no quarantine | Read-only |
| (future) Project-specific adapters | System-specific: artifact schemas, invariants, quarantine bridge | Per adapter spec |

---

## Channel layer

| Module | Purpose | Authority |
|--------|---------|-----------|
| `channels/base.py` | Abstract alert channel interface | None (interface) |
| `channels/telegram.py` | Telegram bot alerts (independent identity) | Write (outbound alerts) |
| `channels/webhook.py` | Generic webhook delivery | Write (outbound alerts) |
| `channels/email.py` | Email alerts | Write (outbound alerts) |
| `channels/stdout.py` | Console output for dev/testing | Write (stdout) |

---

## Authority summary

- **No authority**: engine, modes, scheduler, invariants (data model)
- **Read-only (observation)**: event_reader, process_monitor, config_monitor
- **Read-only (verification)**: policy_engine, integrity
- **Write (guard's own log)**: audit_logger
- **Write (quarantine request via adapter)**: quarantine
- **Write (outbound alerts)**: channels

No module has write access to the protected system's artifacts, configuration, or source code. The only write path to the protected system is the quarantine request, which goes through the adapter's defined mechanism.

---

## Notes

This map will evolve as implementation proceeds. Each module promotion (from planned to implemented) should be tracked and reflected in REPO_NAVIGATION_MAP.
