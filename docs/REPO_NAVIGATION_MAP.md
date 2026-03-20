# CANONICAL SOURCE

# REPO_NAVIGATION_MAP — Aegis Magnum

Purpose: Orient a new developer or AI agent in the repository in under 2 minutes.

---

## 1. What this repo is

Aegis Magnum is a guard architecture framework. It observes, verifies, and alerts on the health and integrity of protected systems. It connects to protected systems via adapters. It does not participate in decision authority.

Core principle: **The guard protects the boundary, not the decision.**

---

## 2. Top-level layout

```
aegis-magnum/
├── docs/               Canon: contracts, invariants, boundaries, discipline
├── bootstrap/          Temporary scaffolding for repo setup (to be replaced by code)
├── core/               (future) Universal guard engine modules
├── adapters/           (future) Project-specific integration layers
├── channels/           (future) Alert delivery (Telegram, webhook, email)
├── config/             (future) Guard configuration and profiles
├── contracts/          (future) Runtime-readable contract definitions
├── tests/              (future) Core and adapter tests
└── README.md           Project entry point
```

Current state: governance skeleton only. Code directories listed above are planned (see [bootstrap/REPO_LAYOUT.md](../bootstrap/REPO_LAYOUT.md)).

---

## 3. Entry points

| What | Where |
|------|-------|
| **First read (human collaborators)** | [../COLLABORATOR_HANDOFF.md](../COLLABORATOR_HANDOFF.md) — after [../README.md](../README.md) |
| **First read (agents)** | [docs/AGENT_ENTRY_CONTRACT.v1.md](AGENT_ENTRY_CONTRACT.v1.md) |
| **Project identity** | [docs/SYSTEM_IDENTITY.md](SYSTEM_IDENTITY.md) |
| **Architectural audit** | [docs/CANON_CORE_FOR_AUDIT.v1.md](CANON_CORE_FOR_AUDIT.v1.md) |
| **Operating rules** | [docs/PROJECT_DISCIPLINE.v1.md](PROJECT_DISCIPLINE.v1.md) |
| **Guard capability** | [docs/SECURITY_BOUNDARY.v1.md](SECURITY_BOUNDARY.v1.md) |
| **Modes** | [docs/MODE_CONTRACT.v1.md](MODE_CONTRACT.v1.md) |
| **Adapter interface** | [docs/ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md) |
| **Roadmap** | [docs/MVP_ROADMAP.md](MVP_ROADMAP.md) |

---

## 4. Where to find what

| I need... | Look here |
|-----------|-----------|
| What the guard may do | [SECURITY_BOUNDARY.v1.md](SECURITY_BOUNDARY.v1.md) |
| What the guard must never do | [AUTHORITY_BOUNDARY.v1.md](AUTHORITY_BOUNDARY.v1.md), [SECURITY_INVARIANTS.v1.md](SECURITY_INVARIANTS.v1.md) |
| Operating modes | [MODE_CONTRACT.v1.md](MODE_CONTRACT.v1.md) |
| Quarantine rules | [QUARANTINE_CONTRACT.v1.md](QUARANTINE_CONTRACT.v1.md) |
| How to connect to a protected system | [ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md) |
| Change rules | [CHANGE_DISCIPLINE.v1.md](CHANGE_DISCIPLINE.v1.md) |
| Document precedence | [CANON_CORE_FOR_AUDIT.v1.md](CANON_CORE_FOR_AUDIT.v1.md) section 5 |
| Threat analysis for a specific system | [SECURITY_RECONNAISSANCE.md](SECURITY_RECONNAISSANCE.md), [VERIFIED_FACTS.md](VERIFIED_FACTS.md), [THREAT_MODEL_DRAFT.md](THREAT_MODEL_DRAFT.md) |
| Unresolved questions | [OPEN_QUESTIONS.md](OPEN_QUESTIONS.md) |
| Future code structure | [bootstrap/REPO_LAYOUT.md](../bootstrap/REPO_LAYOUT.md) |
| Module plan | [bootstrap/INITIAL_MODULE_MAP.md](../bootstrap/INITIAL_MODULE_MAP.md) |
| Implementation roadmap | [MVP_ROADMAP.md](MVP_ROADMAP.md) |
| AI agent rules | [AGENT_ENTRY_CONTRACT.v1.md](AGENT_ENTRY_CONTRACT.v1.md) |
| Document maintenance triggers | [DOCS_MAINTENANCE.md](DOCS_MAINTENANCE.md) |

---

## 5. 2-minute reading path

1. [SYSTEM_IDENTITY.md](SYSTEM_IDENTITY.md) — what this is (30 seconds)
2. [SECURITY_BOUNDARY.v1.md](SECURITY_BOUNDARY.v1.md) — what the guard can do (30 seconds)
3. [MODE_CONTRACT.v1.md](MODE_CONTRACT.v1.md) — operating modes (30 seconds)
4. [ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md) — how it connects (30 seconds)

For deeper understanding, continue with the full reading order in [AGENT_ENTRY_CONTRACT.v1.md](AGENT_ENTRY_CONTRACT.v1.md).

---

## 6. Protected / do not modify without explicit review

- Canonical documents (status: CANONICAL SOURCE) — require version bump for semantic changes.
- Contract documents — require owner review for any authority-related changes.

---

## 7. Document maintenance

This map must be updated when:

- Top-level directories are added or removed.
- New canonical documents are created.
- Entry points or reading path change.
- "Where to find what" targets move or new ones are needed.

See [DOCS_MAINTENANCE.md](DOCS_MAINTENANCE.md) for the full trigger list.
