# EXPORT BOOTSTRAP

# REPO_LAYOUT — Future Code Structure

Status: **EXPORT BOOTSTRAP**
Purpose: Define the planned directory structure for the Aegis Magnum code repository once implementation begins.

---

## Planned layout

```
aegis-magnum/
├── core/
│   ├── engine.py              Main orchestrator: load config, init adapter, run monitors, route events
│   ├── modes.py               Mode state machine (OBSERVE/VERIFY/ALERT/QUARANTINE)
│   ├── scheduler.py           Tick-based or event-driven scheduling for monitors
│   ├── event_reader.py        Universal artifact reader: tail JSONL, cursor/offset, no duplication
│   ├── policy_engine.py       Evaluate invariants against observed state; emit results
│   ├── invariants.py          Base invariant model (InvariantResult: id, severity, status, reason, evidence)
│   ├── integrity.py           File integrity: size monotonicity, hash snapshots, truncation detection
│   ├── process_monitor.py     Process liveness: PID, lock file, command line, service status
│   ├── config_monitor.py      Configuration drift: hash, mtime, drift detection (no secret content in alerts)
│   ├── quarantine.py          Quarantine request handler (delegates to adapter mechanism)
│   └── audit_logger.py        Guard's own audit trail: mode changes, alerts, quarantine lifecycle
│
├── adapters/
│   ├── base.py                Abstract adapter interface (per ADAPTER_CONTRACT.v1.md)
│   ├── generic_jsonl/
│   │   ├── adapter.py         Generic file-based adapter (paths via config)
│   │   └── invariants.py      Minimal invariants (file growth, schema check)
│   └── (future project-specific adapters)
│
├── channels/
│   ├── base.py                Abstract alert channel interface
│   ├── telegram.py            Telegram bot alerts (independent token)
│   ├── webhook.py             Generic webhook alerts
│   ├── email.py               Email alerts
│   └── stdout.py              Console output (development/testing)
│
├── config/
│   ├── aegis.example.yaml     Example configuration file
│   └── profiles/
│       ├── observe.yaml       OBSERVE-only profile
│       ├── verify.yaml        OBSERVE + VERIFY profile
│       └── alert.yaml         Full OBSERVE + VERIFY + ALERT profile
│
├── contracts/                 Runtime-readable copies of canonical contracts (for self-validation)
│
├── audit/                     Guard's own audit artifacts (event logs, mode history, quarantine records)
│
├── tests/
│   ├── core/                  Tests for core modules
│   ├── adapters/              Tests for adapters
│   └── fixtures/              Test data
│
├── docs/                      Canonical documentation (carried from governance skeleton)
│
├── run_aegis.py               Main entrypoint
├── requirements.txt           Python dependencies (pinned)
└── README.md                  Project entry point
```

---

## Design principles for code

- **Core knows nothing about specific protected systems.** All system-specific knowledge lives in adapters.
- **Adapters implement the interface defined in ADAPTER_CONTRACT.** They do not add capabilities beyond what the contract allows.
- **Channels are independent from the protected system's alerting.** The guard should never share a notification identity with the system it monitors.
- **Config profiles map to modes.** Each profile activates a specific mode level.
- **Tests verify invariant logic and adapter conformance.** Not the protected system's behavior.

---

## Notes

This layout will replace the `bootstrap/` directory once code implementation begins. The `docs/` directory carries forward as-is.
