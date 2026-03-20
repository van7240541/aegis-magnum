# CANONICAL SOURCE

# Aegis Magnum

**Full security contour + optional guard framework**

---

## What this is

**Aegis Magnum** is a **general-purpose** security architecture for projects that need a clear **chain-of-trust** model around **any** protected system — decision pipelines, automation, execution infrastructure — not only one product.

It specifies:

- **Trust chain** — people, hosts, secrets, integrations, forensics, incident response.
- **Infrastructure posture** — access, hardening, logging baselines (principles, not vendor-specific runbooks).
- **Secrets and keys** — classification, storage rules, rotation, revocation.
- **Future execution containment** — how automated **external action** must be bounded in any host that introduces it (no execution implementation in this canon).
- **Alignment** with each host product’s own security canon (e.g. `SECURITY_BOUNDARY`, `SECURITY_INVARIANTS`) without replacing it.

**Relationship to examples:** **Opus Magnum** is a **first concrete example** of a protected system whose contracts can be **aligned** with Aegis via [docs/SECURITY_BOUNDARY_ALIGNMENT.md](docs/SECURITY_BOUNDARY_ALIGNMENT.md). Aegis is **not** an “Opus security add-on”; the same documents apply to **other** hosts via **adapters** and host-specific runbooks.

It also preserves the **guard** stance: observe / verify / alert / request boundary actions **only** under explicit contract; **zero decision authority** over the protected system.

**Explicit statements (non-negotiable):**

1. **Aegis is a security contour** — trust chain, secrets, host posture, IR, future execution limits — **not** an application runtime module inside a host repo.
2. **Aegis does not own decision authority** — it does not decide, permit, or execute on behalf of the protected system; the host product’s canon defines that.
3. **Aegis is removable** — a supported protected system must run correctly with Aegis absent or disabled; critical-path dependency on Aegis is a design failure.

**What this folder is not:**

- **Not** a runtime module inside another application’s codebase.
- **Not** a second decision engine or executor for a specific host’s domain.
- **Not** a substitute for the host repository’s `SECURITY_BOUNDARY` or `SECURITY_INVARIANTS` — see [docs/SECURITY_BOUNDARY_ALIGNMENT.md](docs/SECURITY_BOUNDARY_ALIGNMENT.md).

**What this folder is:**

- A **normalized document set** for a **future standalone repository** (copy this tree out as its own repo if desired).
- **Removable**: the protected system must operate without Aegis; if Aegis becomes mandatory in the critical path, the design is wrong.

---

## Core principles

> The guard protects the **boundary**, not the **decision**.

> Aegis describes **security architecture** — infrastructure, secrets, access, future execution limits — and optional guard behavior, **without** inheriting runtime authority.

---

## Root document

Start here for the full model:

- **[docs/SYSTEM_SECURITY_MODEL.v1.md](docs/SYSTEM_SECURITY_MODEL.v1.md)** — trust chain, assets, boundaries, observability, compromise containment.

Supporting canon:

- [docs/SECRETS_AND_KEY_MANAGEMENT.v1.md](docs/SECRETS_AND_KEY_MANAGEMENT.v1.md)
- [docs/SERVER_HARDENING_BASELINE.v1.md](docs/SERVER_HARDENING_BASELINE.v1.md)
- [docs/FUTURE_EXECUTION_SECURITY.v1.md](docs/FUTURE_EXECUTION_SECURITY.v1.md)
- [docs/INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md](docs/INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md)
- [docs/SECURITY_BOUNDARY_ALIGNMENT.md](docs/SECURITY_BOUNDARY_ALIGNMENT.md)

Draft (interface research only):

- [docs/ADAPTER_CONTRACT.v1.md](docs/ADAPTER_CONTRACT.v1.md)
- [docs/ADAPTER_RESEARCH.v1.md](docs/ADAPTER_RESEARCH.v1.md)

---

## First-read for a new collaborator

Read in this **exact order** (security engineer or implementer):

1. [README.md](README.md) — this file.
2. [COLLABORATOR_HANDOFF.md](COLLABORATOR_HANDOFF.md) — mission, breach rules, uncertainty defaults, first deliverable.
3. [docs/SYSTEM_SECURITY_MODEL.v1.md](docs/SYSTEM_SECURITY_MODEL.v1.md)
4. [docs/SECURITY_BOUNDARY_ALIGNMENT.md](docs/SECURITY_BOUNDARY_ALIGNMENT.md)
5. [docs/FUTURE_EXECUTION_SECURITY.v1.md](docs/FUTURE_EXECUTION_SECURITY.v1.md)
6. [docs/SECRETS_AND_KEY_MANAGEMENT.v1.md](docs/SECRETS_AND_KEY_MANAGEMENT.v1.md)
7. [docs/SERVER_HARDENING_BASELINE.v1.md](docs/SERVER_HARDENING_BASELINE.v1.md)
8. [docs/INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md](docs/INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md)
9. [docs/ADAPTER_CONTRACT.v1.md](docs/ADAPTER_CONTRACT.v1.md) (draft)
10. [docs/ADAPTER_RESEARCH.v1.md](docs/ADAPTER_RESEARCH.v1.md) (draft)
11. [docs/MVP_ROADMAP.md](docs/MVP_ROADMAP.md)
12. [docs/REPO_NAVIGATION_MAP.md](docs/REPO_NAVIGATION_MAP.md)

---

## What this system will NEVER do

- Participate in **decision authority** for the protected system.
- Store or transmit **real secrets** inside these canonical documents.
- Prescribe **domain execution logic**, **vendor API usage**, or concrete **executor implementations**.
- Require **any named host product’s** runtime paths as conditions of this export’s validity.

---

## Current status

Governance and security-architecture **documents only** — no runtime code in this tree. Implementation phases: [docs/MVP_ROADMAP.md](docs/MVP_ROADMAP.md).

---

## Optional: collaboration workspaces (ChatGPT Projects, boards, etc.)

If you split work across **multiple project containers** (chats + instructions + files per theme), use **[docs/COLLABORATION_WORKSPACE.v1.md](docs/COLLABORATION_WORKSPACE.v1.md)** as the map:

- **Main Line** — priorities, handoff, integration ([README](README.md), [COLLABORATOR_HANDOFF](COLLABORATOR_HANDOFF.md), [SYSTEM_SECURITY_MODEL](docs/SYSTEM_SECURITY_MODEL.v1.md), [MVP_ROADMAP](docs/MVP_ROADMAP.md)).
- **Canon & Governance** — Aegis security canon (secrets, hardening, IR, future execution, alignment) — **not** a copy of host `SECURITY_BOUNDARY` (that stays in the protected system’s repo).
- **Observe Core** — first OBSERVE-only deliverable.
- **Adapter Architecture** — universal adapter + anti-drift.
- **Opus Adapter** — first host example only ([SECURITY_BOUNDARY_ALIGNMENT](docs/SECURITY_BOUNDARY_ALIGNMENT.md)).
- **Threat Model & Validation** — evidence track; not shipped as files in this v1 tree (see doc).

The **git repository** remains the **single source of truth** for canon text; projects are for **coordination**, not parallel canons.

**Hebrew summary (draft):** [docs/COLLABORATION_WORKSPACE.he.v1.md](docs/COLLABORATION_WORKSPACE.he.v1.md)

---

## Quick diagram

```text
Trust chain (humans, keys, hosts, integrations)
        │
        ▼
SYSTEM_SECURITY_MODEL  ←── SECRETS / HARDENING / IR / FUTURE_EXECUTION
        │
        ▼
Host product canon (SECURITY_BOUNDARY, SECURITY_INVARIANTS, …)  ←── ALIGNMENT doc
        │
        ▼
Optional Aegis guard (observe / verify / alert) — removable, non-authoritative
```
