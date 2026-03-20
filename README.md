# EXPORT BOOTSTRAP

# Aegis Magnum

**Guard Architecture Framework**

---

## What is this

Aegis Magnum is a universal guard system for protecting decision and execution infrastructure. It observes, verifies, and alerts on the health and integrity of protected systems. When explicitly authorized, it may request quarantine at the boundary.

It is designed to be connected to any system via adapters — not hardwired to a specific project.

**What this folder is:**

- **Not** a runtime module inside another application’s codebase.
- **Not** a second decision engine — the guard protects **integrity at the boundary**, not **authority over decisions**.
- **An export-ready governance skeleton** for a **future standalone repository** (this tree may be copied out as its own Git repo).
- **Discipline before code** — canonical contracts and reading order matter more than early implementation.

---

## Core principle

> The guard protects the boundary, not the decision.
> It enforces integrity, not authority.

---

## What this system will NEVER do

- It will **not** make decisions for the protected system.
- It will **not** override the protected system's execution.
- It will **not** modify the protected system's artifacts, configuration, or source code.
- It will **not** act without visibility — every action produces an audit record.
- It will **not** acquire enforcement capability without an explicit versioned contract.
- It will **not** operate as a second decision engine.

---

## Current status

This repository contains the **governance skeleton** — canonical contracts, invariants, and discipline documents. No runtime code exists yet. See [docs/MVP_ROADMAP.md](docs/MVP_ROADMAP.md) for the implementation plan.

---

## First-read for new collaborator

Use this order so you never have to guess whether this is part of another product, whether you may touch another system’s runtime, or whether you may enforce without a contract.

**Human engineers:** read **[COLLABORATOR_HANDOFF.md](COLLABORATOR_HANDOFF.md)** immediately after this README — mission, your role, uncertainty defaults, anti-patterns, **first deliverable (OBSERVE-only, no enforcement)**, definition of success, and final design rules.

**Everyone (humans and agents)** then reads, in order:

1. `README.md` — project face, scope, global prohibitions.
2. [docs/AGENT_ENTRY_CONTRACT.v1.md](docs/AGENT_ENTRY_CONTRACT.v1.md) — entry discipline; mandatory doc order for agents (humans should follow it too).
3. [docs/PROJECT_DISCIPLINE.v1.md](docs/PROJECT_DISCIPLINE.v1.md) — operational law of the repo.
4. [docs/AUTHORITY_BOUNDARY.v1.md](docs/AUTHORITY_BOUNDARY.v1.md) — zones; ban on silent influence.
5. [docs/SECURITY_BOUNDARY.v1.md](docs/SECURITY_BOUNDARY.v1.md) — what the guard may and may not do.
6. [docs/SECURITY_INVARIANTS.v1.md](docs/SECURITY_INVARIANTS.v1.md) — non-negotiable invariants.
7. [docs/MODE_CONTRACT.v1.md](docs/MODE_CONTRACT.v1.md) — OBSERVE / VERIFY / ALERT / QUARANTINE / BLOCK.
8. [docs/ADAPTER_CONTRACT.v1.md](docs/ADAPTER_CONTRACT.v1.md) — how the guard connects to a protected system.
9. [docs/QUARANTINE_CONTRACT.v1.md](docs/QUARANTINE_CONTRACT.v1.md) — quarantine as request, not command.
10. [bootstrap/REPO_LAYOUT.md](bootstrap/REPO_LAYOUT.md) — planned code layout (`core/`, `adapters/`, `channels/`, `contracts/`, `audit/`).
11. [bootstrap/INITIAL_MODULE_MAP.md](bootstrap/INITIAL_MODULE_MAP.md) — module responsibilities and authority levels.
12. [docs/MVP_ROADMAP.md](docs/MVP_ROADMAP.md) — staged implementation plan.

After that, use [docs/REPO_NAVIGATION_MAP.md](docs/REPO_NAVIGATION_MAP.md) for day-to-day lookup.

---

## Quick orientation

| Document | Purpose |
|----------|---------|
| [docs/SYSTEM_IDENTITY.md](docs/SYSTEM_IDENTITY.md) | What this project is and is not |
| [docs/SECURITY_BOUNDARY.v1.md](docs/SECURITY_BOUNDARY.v1.md) | What the guard may and may not do |
| [docs/MODE_CONTRACT.v1.md](docs/MODE_CONTRACT.v1.md) | Operating modes (OBSERVE / VERIFY / ALERT / QUARANTINE / BLOCK) |
| [docs/ADAPTER_CONTRACT.v1.md](docs/ADAPTER_CONTRACT.v1.md) | How to connect to a protected system |
| [docs/REPO_NAVIGATION_MAP.md](docs/REPO_NAVIGATION_MAP.md) | Full repository orientation |

For **AI agents**: follow [docs/AGENT_ENTRY_CONTRACT.v1.md](docs/AGENT_ENTRY_CONTRACT.v1.md) (mandatory reading order there includes `SYSTEM_IDENTITY` and `CANON_CORE` — do not skip).

For **human collaborators**: [COLLABORATOR_HANDOFF.md](COLLABORATOR_HANDOFF.md) plus the first-read list above.

---

## Architecture

```
Protected System (owns all decision authority)
    |
    | emits artifacts, logs, process state
    v
Aegis Magnum Core (observes, verifies, alerts)
    |
    | via adapter
    v
Project-specific invariants and quarantine mechanism
    |
    | produces
    v
Alerts / evidence / quarantine requests (to operator)
```

---

## Key documents

### Onboarding

- [COLLABORATOR_HANDOFF.md](COLLABORATOR_HANDOFF.md) — human handoff: mission, scope, allowed/forbidden work, first implementation target, definition of success

### Governance (CANONICAL SOURCE)

- `PROJECT_DISCIPLINE.v1.md` — operational law
- `SECURITY_INVARIANTS.v1.md` — non-negotiable invariants
- `SECURITY_BOUNDARY.v1.md` — guard capability boundary
- `AUTHORITY_BOUNDARY.v1.md` — zone permissions and prohibitions
- `MODE_CONTRACT.v1.md` — operating mode definitions
- `QUARANTINE_CONTRACT.v1.md` — quarantine semantics
- `ADAPTER_CONTRACT.v1.md` — integration interface
- `CHANGE_DISCIPLINE.v1.md` — change rules

### Thinking layer (NON-CANONICAL DRAFT)

- `SECURITY_RECONNAISSANCE.md` — observation registry
- `VERIFIED_FACTS.md` — evidence registry
- `THREAT_MODEL_DRAFT.md` — risk assessment
- `OPEN_QUESTIONS.md` — architecture blockers

### Bootstrap (EXPORT BOOTSTRAP)

- `bootstrap/REPO_LAYOUT.md` — future code structure
- `bootstrap/INITIAL_MODULE_MAP.md` — module inventory
- `MVP_ROADMAP.md` — implementation roadmap
