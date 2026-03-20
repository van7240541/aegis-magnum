# CANONICAL SOURCE

# REPO_NAVIGATION_MAP — Aegis Magnum

**Purpose:** Orient a security engineer or developer in **under two minutes**.

---

## 1. What this repo is

**Aegis Magnum** is a **full security contour** (trust chain, secrets, host baseline, IR, future execution containment) plus an optional **guard** that observes / verifies / alerts **without decision authority**. It is **system-agnostic** and **independent of any host runtime**.

Core alignment with a product that has its own `SECURITY_BOUNDARY` / `SECURITY_INVARIANTS`: [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md).

---

## 2. Layout (this export)

```
exports/aegis_magnum/
├── README.md
├── COLLABORATOR_HANDOFF.md
└── docs/
    ├── SYSTEM_SECURITY_MODEL.v1.md      ← start here (root)
    ├── SECRETS_AND_KEY_MANAGEMENT.v1.md
    ├── SERVER_HARDENING_BASELINE.v1.md
    ├── FUTURE_EXECUTION_SECURITY.v1.md
    ├── INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md
    ├── SECURITY_BOUNDARY_ALIGNMENT.md
    ├── ADAPTER_CONTRACT.v1.md           (draft)
    ├── ADAPTER_RESEARCH.v1.md           (draft)
    ├── MVP_ROADMAP.md
    ├── COLLABORATION_WORKSPACE.v1.md    (optional ChatGPT / multi-project map)
    └── REPO_NAVIGATION_MAP.md           (this file)
```

**Future code** (when implemented) should live in a **separate** tree (`core/`, `adapters/`, etc.) in the standalone repo — not required for this governance export.

---

## 3. Entry points

| Need | Document |
|------|----------|
| **First human read** | [../COLLABORATOR_HANDOFF.md](../COLLABORATOR_HANDOFF.md) after [../README.md](../README.md) |
| **Root security model** | [SYSTEM_SECURITY_MODEL.v1.md](SYSTEM_SECURITY_MODEL.v1.md) |
| **How Aegis relates to Opus/host canon** | [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md) |
| **Secrets** | [SECRETS_AND_KEY_MANAGEMENT.v1.md](SECRETS_AND_KEY_MANAGEMENT.v1.md) |
| **VPS / host** | [SERVER_HARDENING_BASELINE.v1.md](SERVER_HARDENING_BASELINE.v1.md) |
| **Future execution limits** | [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md) |
| **Leak / compromise** | [INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md](INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md) |
| **Adapter interface (draft)** | [ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md) |
| **Roadmap** | [MVP_ROADMAP.md](MVP_ROADMAP.md) |
| **Optional multi-container collaboration map** | [COLLABORATION_WORKSPACE.v1.md](COLLABORATION_WORKSPACE.v1.md) |

---

## 4. Two-minute reading path

1. [../README.md](../README.md) then [../COLLABORATOR_HANDOFF.md](../COLLABORATOR_HANDOFF.md)
2. [SYSTEM_SECURITY_MODEL.v1.md](SYSTEM_SECURITY_MODEL.v1.md) — trust chain and boundaries.
3. [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md) — non-replacement of host SECURITY_BOUNDARY.
4. [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md) — future execution as high-risk boundary.

Full order: see [../README.md](../README.md) § First-read (12 steps).

---

## 5. Document labels

- Lines starting with `# CANONICAL SOURCE` — binding governance for this export.
- Lines starting with `# DRAFT` — not yet promoted; subject to change.

---

## 6. Maintenance

Update this map when documents are added, removed, or renamed.

---

**Version:** v1
