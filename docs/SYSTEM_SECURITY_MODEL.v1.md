# CANONICAL SOURCE

# SYSTEM_SECURITY_MODEL v1

**Scope:** Root security architecture for Aegis Magnum. Defines the **full trust-chain model** (people, hosts, secrets, integrations, future execution) independent of any single protected application. This document does **not** grant decision authority to Aegis and does **not** replace a protected system’s own `SECURITY_BOUNDARY` or `SECURITY_INVARIANTS` — see [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md).

---

## 1. Purpose

Aegis Magnum is documented here as:

- A **security contour**: infrastructure access, secrets lifecycle, host posture, authority separation, future execution containment, observability, and incident response.
- **Non-invasive** with respect to protected runtime: no requirement to embed Aegis inside decision code; Aegis must remain **removable** without breaking the protected system’s supported operation.
- **System-agnostic**: no dependency on a specific domain stack, vendor tree, or file layout in canon text (concrete paths belong in deployment runbooks outside this export, or in non-canonical appendices).

---

## 2. Trust chain model

Trust flows through explicit boundaries. Nothing is trusted by default.

```text
Human operators ──► identity providers (email, Git, cloud, VPS panel)
       │
       ▼
Secrets & keys ──► least privilege, rotation, revocation
       │
       ▼
Hosts & network ──► SSH, firewall, patching, minimized services
       │
       ▼
Integrations ──► APIs, bots, webhooks (each a separate trust boundary)
       │
       ▼
Protected system ──► owns decision / permission / execution policy
       │
       ▼
Aegis guard (optional) ──► observe / verify / alert / request boundary actions
       │
       ▼
Forensics ──► audit trails, correlation, incident response
```

**Rule:** Compromise at any layer must be **containable** without assuming compromise of all others. See [INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md](INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md).

---

## 3. Asset classification

| Class | Examples | Treatment |
|-------|------------|-----------|
| **Critical secrets** | SSH private keys, API keys, signing material, bot tokens, credentials for privileged external action | Never in version control; inventory; rotation; scoped access — [SECRETS_AND_KEY_MANAGEMENT.v1.md](SECRETS_AND_KEY_MANAGEMENT.v1.md) |
| **Infrastructure** | VPS, DNS, TLS certs, firewall rules | Hardened baseline; change-controlled — [SERVER_HARDENING_BASELINE.v1.md](SERVER_HARDENING_BASELINE.v1.md) |
| **Identity & access** | GitHub org, provider panels, email for recovery | MFA where available; separate accounts per role |
| **Protected system authority** | Decision outputs, permission verdicts, execution intents | Owned **only** by the protected system; Aegis does not originate or rewrite these |
| **Aegis artifacts** | Guard audit log, alerts, adapter metadata | Integrity and retention policy; separate from protected truth layer |
| **Future execution path** | Any bridge from intent to external effect | High risk; not presupposed — [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md) |

---

## 4. Trust boundaries (summary)

1. **Operator ↔ infrastructure:** SSH and panel access are high-value; keys-only, no shared root, logging.
2. **Repository ↔ CI/CD:** branch protection, no secrets in repo, review for authority-related changes.
3. **Host ↔ network:** default deny; expose only required ports; monitor auth failures.
4. **Secret ↔ process:** a process may only receive the minimal secret material for its role; no “god” env file for all roles.
5. **Guard ↔ protected system:** read-oriented observation by default; any enforcement or quarantine is explicit, contracted, and auditable — alignment with host product canon is described in [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md).
6. **External agent (e.g. future bot) ↔ execution:** treated as **untrusted** until constrained by policy; never co-extensive with decision authority.

---

## 5. Authority separation (non-negotiable)

- **Signal ≠ permission ≠ execution.** Aegis does not collapse these layers.
- **No hidden authority:** any action that changes protected behavior must be visible, attributable, and justified by an explicit mode or contract on the guard side, without substituting for the protected system’s own authority model.
- **Fail-closed for external automation:** if a guard or adapter is uncertain, it does not expand privilege. Document and escalate (see [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md)).

---

## 6. Secrets as high-risk objects

Secrets are **liabilities**, not convenience. Central expectations:

- Inventory every secret type (SSH, Git, cloud, messaging, API, keys for external execution or privileged APIs).
- No canonical document in this tree contains real secret values or live config snippets with credentials.
- Rotation and revocation are **procedures**, not ad-hoc edits — [SECRETS_AND_KEY_MANAGEMENT.v1.md](SECRETS_AND_KEY_MANAGEMENT.v1.md), [INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md](INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md).

---

## 7. Execution as future high-risk component

**Today:** no execution layer is assumed in Aegis canon. **Future:** any path that could move from “observed intent” to “external effect” is a **separate trust boundary** requiring validation, caps, kill switch, and explicit contracts — [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md).

---

## 8. Compromise containment model

- **Assume breach:** design for partial compromise (stolen key, rogue process, leaked token).
- **Blast radius:** separate keys per role; separate channels for alerts vs. operational bots where feasible.
- **Recovery:** revoke → rotate → verify → restore service — [INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md](INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md).

---

## 9. Observability requirement

Operators must be able to answer, without guesswork:

- Who authenticated to which system and when.
- What configuration or secret scope changed.
- What the guard observed, verified, and alerted (guard-owned audit).

Baseline expectations: [SERVER_HARDENING_BASELINE.v1.md](SERVER_HARDENING_BASELINE.v1.md) (host logging); guard implementation must emit structured audit events when code exists.

---

## 10. Document map (this export)

| Document | Role |
|----------|------|
| This file | Root model |
| [SECRETS_AND_KEY_MANAGEMENT.v1.md](SECRETS_AND_KEY_MANAGEMENT.v1.md) | Secrets lifecycle |
| [SERVER_HARDENING_BASELINE.v1.md](SERVER_HARDENING_BASELINE.v1.md) | Host posture |
| [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md) | Execution containment (future) |
| [INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md](INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md) | IR and key events |
| [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md) | Relation to a host product’s security canon |
| [ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md) | Adapter interface (draft) |
| [ADAPTER_RESEARCH.v1.md](ADAPTER_RESEARCH.v1.md) | Adapter research notes (draft) |
| [MVP_ROADMAP.md](MVP_ROADMAP.md) | Staged delivery |
| [REPO_NAVIGATION_MAP.md](REPO_NAVIGATION_MAP.md) | Orientation |
| [COLLABORATION_WORKSPACE.v1.md](COLLABORATION_WORKSPACE.v1.md) | Optional ChatGPT / multi-container map |
| [MAIN_LINE_PROJECT_INSTRUCTION.v1.md](MAIN_LINE_PROJECT_INSTRUCTION.v1.md) | Main Line project instruction (paste) |
| [GITHUB_REPOSITORY_ABOUT.v1.md](GITHUB_REPOSITORY_ABOUT.v1.md) | Suggested GitHub **About** text |
| [OBSERVE_CORE_ARCHITECTURE_SKETCH.v1.md](OBSERVE_CORE_ARCHITECTURE_SKETCH.v1.md) | Observe-first code sketch (docs only) |

---

## 11. Precedence

If a lower-level document appears to expand Aegis authority beyond this root model, **this document and [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md) win** until reconciled by explicit canon revision.

**Version:** v1
