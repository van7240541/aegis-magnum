# CANONICAL SOURCE

# COLLABORATION_WORKSPACE v1

**Scope:** Optional way to split **coordination** across multiple workspace containers (e.g. ChatGPT Projects, GitHub Project boards, or team channels) **without** splitting this repository into six repos. This document maps **roles** to **files that exist in Aegis Magnum v1 canon** and states what lives **only in a host product** (e.g. Opus Magnum).

**Rule:** A **project** here is a **container for chats, files, and instructions** — not a second canon. The **source of truth** for Aegis text remains this git tree.

---

## Relationship to canon v1

- **Root model:** [SYSTEM_SECURITY_MODEL.v1.md](SYSTEM_SECURITY_MODEL.v1.md) (not a separate `SYSTEM_IDENTITY` file).
- **Security + governance for Aegis:** secrets, hardening, future execution, IR, alignment — files listed in [README.md](../README.md).
- **Host application canon** (`SECURITY_BOUNDARY`, `SECURITY_INVARIANTS`, modes, quarantine semantics) stays in the **protected system’s repository** — referenced via [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md).
- **No `bootstrap/`** in this export; first code layout is described in [MVP_ROADMAP.md](MVP_ROADMAP.md).
- **Threat / reconnaissance / open-questions** drafts are **not** in this tree; they may live in a host repo or a separate evidence project — see §6.

---

## 1. Aegis Magnum — Main Line

**Purpose:** Full picture, priorities, final architectural decisions, handoff, links to other tracks.

**Primary files in this repo:**

| File | Role |
|------|------|
| [README.md](../README.md) | Project face, non-negotiables |
| [COLLABORATOR_HANDOFF.md](../COLLABORATOR_HANDOFF.md) | Human entry, breach rules, first deliverable |
| [SYSTEM_SECURITY_MODEL.v1.md](SYSTEM_SECURITY_MODEL.v1.md) | Root trust-chain and asset model |
| [REPO_NAVIGATION_MAP.md](REPO_NAVIGATION_MAP.md) | Orientation |
| [MVP_ROADMAP.md](MVP_ROADMAP.md) | Staged delivery |

**Project instruction (summary):** Coordinate integration and prioritization; do not invent authority; do not mix planning, implementation, and validation in one thread; route host-specific detail to Adapter / Opus tracks.

---

## 2. Aegis Magnum — Canon & Governance (Aegis security canon)

**Purpose:** Non-negotiable **Aegis** security rules — trust chain, secrets, host baseline, execution containment, IR.

**Primary files in this repo:**

| File | Role |
|------|------|
| [SYSTEM_SECURITY_MODEL.v1.md](SYSTEM_SECURITY_MODEL.v1.md) | Root |
| [SECRETS_AND_KEY_MANAGEMENT.v1.md](SECRETS_AND_KEY_MANAGEMENT.v1.md) | Secrets lifecycle |
| [SERVER_HARDENING_BASELINE.v1.md](SERVER_HARDENING_BASELINE.v1.md) | Host policy |
| [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md) | Future execution boundary (universal) |
| [INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md](INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md) | IR |
| [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md) | How Aegis relates to **host** `SECURITY_BOUNDARY` / invariants |

**Not in Aegis repo:** Host-only documents such as application `SECURITY_BOUNDARY`, `SECURITY_INVARIANTS`, `MODE_CONTRACT`, `QUARANTINE_CONTRACT` — those are **host canon**, not duplicated here as parallel canon.

---

## 3. Aegis Magnum — Observe Core

**Purpose:** First real deliverable: **OBSERVE-only** guard skeleton; audit sink; success criteria per [COLLABORATOR_HANDOFF.md](../COLLABORATOR_HANDOFF.md) §10.

**Primary files in this repo:**

| File | Role |
|------|------|
| [COLLABORATOR_HANDOFF.md](../COLLABORATOR_HANDOFF.md) | Strict first deliverable |
| [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md) | No premature execution |
| [ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md) (draft) | Read-only / structural adapter scope |
| [MVP_ROADMAP.md](MVP_ROADMAP.md) | Stages 0–1 |

---

## 4. Aegis Magnum — Adapter Architecture

**Purpose:** Universal adapter rules; prevent domain leakage and adapter drift into a second decision layer.

**Primary files in this repo:**

| File | Role |
|------|------|
| [ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md) (draft) | Interface + anti-drift §2 |
| [ADAPTER_RESEARCH.v1.md](ADAPTER_RESEARCH.v1.md) (draft) | Research notes |
| [SYSTEM_SECURITY_MODEL.v1.md](SYSTEM_SECURITY_MODEL.v1.md) | Trust boundaries |
| [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md) | Execution abstraction |

---

## 5. Aegis Magnum — Opus Adapter (first host example)

**Purpose:** **Only** how Aegis attaches to **Opus Magnum** as first protected-system example — not redefining universal Aegis.

**Primary files in this repo:**

| File | Role |
|------|------|
| [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md) | Non-replacement of host canon; Opus as example |

**Optional later:** host-specific notes (e.g. `OPUS_ADAPTER_NOTES.md`) in **host repo** or a dedicated integration repo — **not** universal canon.

**Host canon for Opus:** remains in **Opus Magnum** repository (`docs/CONTRACTS/`, etc.).

---

## 6. Aegis Magnum — Threat Model & Validation

**Purpose:** Evidence, reconnaissance, verified facts, threat drafts, open questions, validation of observe-layer value.

**In this Aegis v1 export:** these document **types are not included**. Run this track using:

- Operational tickets / spreadsheets, or  
- Documents in the **host** repository, or  
- A separate evidence-only folder or repo linked from Main Line.

Do **not** treat missing files here as permission to skip evidence discipline — only as **placement** outside this canon tree.

---

## Suggested creation order (for workspace containers)

1. Main Line  
2. Canon & Governance (Aegis security)  
3. Observe Core  
4. Adapter Architecture  
5. Opus Adapter  
6. Threat Model & Validation  

---

## Sharing guidance

- **Collaborators:** Main Line, Observe Core, Adapter Architecture, Opus Adapter, Threat Model — as needed.  
- **Canon & Governance (Aegis):** share read-only or with owners who respect change discipline; prefer **you** retain merge authority on meaning.

---

**Version:** v1
