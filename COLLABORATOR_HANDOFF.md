# EXPORT BOOTSTRAP

# COLLABORATOR_HANDOFF — Human entry

**Scope:** Operational onboarding for human engineers. Does not replace binding contracts in `docs/`; use this file to orient, then obey the canonical documents.

---

## 1. Mission

Build **Aegis Magnum**: a guard framework that attaches **outside** a protected system, observes and verifies its boundary health, alerts operators, and — only under explicit contract and mode — requests quarantine via the protected system’s own operator/emergency mechanism.

You are **not** building a feature inside someone else’s runtime. You are building a **separate product** whose first incarnation is this governance skeleton, then code under `core/`, `adapters/`, `channels/`, `audit/` as in [bootstrap/REPO_LAYOUT.md](bootstrap/REPO_LAYOUT.md).

---

## 2. Your role in this system

You are **not** extending any protected system’s core application, decision pipeline, or product repository as if you were on that team’s runtime roadmap.

You **are** designing an **external** guard that:

- observes boundary-relevant signals;
- verifies them against contracts and adapter-defined invariants;
- alerts operators;
- requests boundary restriction (quarantine) **only** through mechanisms the protected system already owns, via the adapter.

You **do not** own:

- decision logic inside the protected system;
- risk or safety **computation** that belongs to that system (you may only **verify** stated outputs against canon, where applicable);
- permission or eligibility semantics;
- execution authority (placing trades, submitting transactions, approving intents, etc.).

You **are** responsible for:

- guard architecture and module boundaries;
- adapter contracts and adapter implementations (read paths, invariant definitions, quarantine **request** formatting);
- guard-local **auditability** (mode changes, alerts, quarantine lifecycle on the guard side);
- ensuring checks remain **enforcement-separated**: detection must not silently become authority.

This section fixes **your behavior**, not only the system’s shape.

---

## 3. Non-goals

You must **not** build:

- A second decision engine, risk engine, or permission layer for any protected system.
- Anything that rewrites, forges, or “fixes” the protected system’s artifacts or configuration.
- Silent or timer-driven enforcement without operator visibility and audit.
- A “security bot” that trades, routes orders, or interprets domain data into trading or business **decisions** for the protected system.
- Coupling that requires importing or executing the protected system’s application code inside the guard.

---

## 4. Architectural boundary

| Zone | Protected system | Aegis Magnum |
|------|------------------|--------------|
| Decision / permission / risk | **Owns all authority** | No participation |
| Artifacts (logs, events, truth layer) | **Owns writes** | Read-only observation (unless canon explicitly allows otherwise) |
| Quarantine | **Owns the mechanism** | May only **request** via adapter-defined path |
| Alerts | Own channel(s) | **Separate** channel identity where possible |

The guard **ends** where influence would change *what* the protected system decides. It **begins** at observable boundary signals: process liveness, artifact integrity, config fingerprints, invariant checks, and operator-facing alerts.

Full detail: [docs/AUTHORITY_BOUNDARY.v1.md](docs/AUTHORITY_BOUNDARY.v1.md), [docs/SECURITY_BOUNDARY.v1.md](docs/SECURITY_BOUNDARY.v1.md).

---

## 5. Allowed work

You **may** design and implement:

- **Core**: engine shell, modes, scheduling, event/artifact reading, policy evaluation, integrity/process/config monitors, guard-local audit logger.
- **Adapters**: discovery, artifact sources, critical files, invariant list, process spec, quarantine capability per [docs/ADAPTER_CONTRACT.v1.md](docs/ADAPTER_CONTRACT.v1.md).
- **Channels**: independent alerting (e.g. Telegram, webhook, email, stdout).
- **Invariant engine**: evaluate adapter-defined checks; emit structured results and alerts.
- **Audit trail**: guard-owned log of mode changes, alerts, quarantine request lifecycle (not the protected system’s truth layer).
- **Quarantine request path**: thin bridge that formats and submits a **request** per [docs/QUARANTINE_CONTRACT.v1.md](docs/QUARANTINE_CONTRACT.v1.md).

Default implementation stance after the **first deliverable**: **VERIFY + ALERT** as explicit next steps. **QUARANTINE** only after contracts and tests are in place.

---

## 6. Forbidden work

You **must not**:

- Modify any protected system’s **runtime** application code, vendor tree, or deployment secrets to “make the guard work.”
- Introduce **hidden authority**: new writes, side effects, or enforcement not listed in a versioned contract.
- Rewrite or inject **intents**, **decisions**, or **events** in the protected system’s streams.
- Change **decision**, **risk**, or **permission** semantics of a protected system from the guard.
- Enable **BLOCK** mode or execution interposition without a future `ENFORCEMENT_CONTRACT` (not defined in v1).
- Expand scope without updating the relevant canonical doc and [docs/CHANGE_DISCIPLINE.v1.md](docs/CHANGE_DISCIPLINE.v1.md) classification.

**Violating any of the above is a boundary breach, not an implementation mistake.** It is not excused by good intent, tight deadlines, or “we will document it later.” Stop, revert or do not merge, and escalate.

---

## 7. If you are unsure

If any design or PR risks:

- influencing the protected system’s **decision** logic or outcomes;
- **modifying** its artifacts or configuration;
- introducing **hidden authority** (side effects, writes, enforcement paths not in contract);

**Default action:**

1. **Do not implement** the risky part.
2. **Document** the question in [docs/OPEN_QUESTIONS.md](docs/OPEN_QUESTIONS.md) (or your project’s equivalent tracking doc).
3. **Proceed only** after boundary clarification — ideally a contract or owner decision recorded in canon.

Uncertainty favors **no action** on the guard side. The protected system may continue to operate; the guard must not “fill the gap” with improvised authority.

---

## 8. What a bad implementation looks like

Any of the following indicates a **violation of system design** (not a style issue):

- The guard **modifies or rewrites** the protected system’s decision or audit artifacts.
- The guard introduces its **own** decision, permission, or risk logic that competes with the protected system’s authority.
- The guard **silently** blocks, drops, or rewrites execution or intents without operator visibility and contract.
- The guard becomes **required** for the protected system to start, run, or complete its normal job (hard dependency in the critical path).
- The guard **cannot be removed or disabled** without breaking the protected system’s documented, supported operation.
- The guard shares a single notification identity with the protected system such that **one compromise silences both**.

Use this list as an **anti-pattern checklist** before merge.

---

## 9. Required reading order

Read in this order before writing code:

1. [README.md](README.md)
2. [docs/AGENT_ENTRY_CONTRACT.v1.md](docs/AGENT_ENTRY_CONTRACT.v1.md) (entry discipline — applies to humans too)
3. [docs/PROJECT_DISCIPLINE.v1.md](docs/PROJECT_DISCIPLINE.v1.md)
4. [docs/AUTHORITY_BOUNDARY.v1.md](docs/AUTHORITY_BOUNDARY.v1.md)
5. [docs/SECURITY_BOUNDARY.v1.md](docs/SECURITY_BOUNDARY.v1.md)
6. [docs/SECURITY_INVARIANTS.v1.md](docs/SECURITY_INVARIANTS.v1.md)
7. [docs/MODE_CONTRACT.v1.md](docs/MODE_CONTRACT.v1.md)
8. [docs/ADAPTER_CONTRACT.v1.md](docs/ADAPTER_CONTRACT.v1.md)
9. [docs/QUARANTINE_CONTRACT.v1.md](docs/QUARANTINE_CONTRACT.v1.md)
10. [bootstrap/REPO_LAYOUT.md](bootstrap/REPO_LAYOUT.md)
11. [bootstrap/INITIAL_MODULE_MAP.md](bootstrap/INITIAL_MODULE_MAP.md)
12. [docs/MVP_ROADMAP.md](docs/MVP_ROADMAP.md)

Then use [docs/REPO_NAVIGATION_MAP.md](docs/REPO_NAVIGATION_MAP.md) for ongoing lookup.

---

## 10. First deliverable (strict)

The **first** merged implementation must be a **minimal guard skeleton** that:

- runs in **OBSERVE mode only** (no VERIFY / ALERT / QUARANTINE in the same deliverable unless explicitly approved as a separate, scoped change);
- produces **structured audit events** in the guard’s **own** audit sink (format defined in code, must be append-only and reviewable);
- **does not modify or influence** the protected system (read-only observation paths only);
- **demonstrates** the adapter interface (e.g. stub + generic paths-from-config) **without** any enforcement or quarantine path.

**Explicitly out of scope for the first deliverable:** quarantine, blocking, interposition, writing to protected artifacts, changing protected configuration, or any mode above OBSERVE.

### Definition of success (first deliverable)

The first deliverable is considered **successful** only if **all** of the following are true:

- It produces a **stable, reproducible** audit artifact (same inputs / observation window → same structured records in the guard’s sink, modulo explicit timestamps).
- It **does not alter** the behavior of the protected system (no measurable change when the guard is on vs off, aside from normal read I/O if applicable).
- It can be **fully disabled** with **no impact** on the protected system’s supported runtime (startup, steady operation, and shutdown do not depend on the guard).
- It **reveals at least one valid observe signal** in the observed data (see below — this proves the observe layer is not vacuous).

**Valid observe signal** (criterion 4 — all must hold for the finding to count):

- **Reproducible** — same procedure and window → same conclusion (modulo documented nondeterminism).
- **Non-obvious from raw artifacts alone** — not something an operator would routinely infer by skimming the same files without the guard’s structured check, join, or aggregation (the layer must add **seeing**, not restate the obvious).
- **Structural inconsistency *or* stable pattern** — either a broken invariant / impossible state / missing link / systematic drift, **or** a pattern that holds across a **defined** observation window (not a one-off glitch passed off as insight).

**Non-trivial** here means: **it changes understanding of the system** — if the finding would not affect how you trust or interpret the protected system’s behavior, it does not satisfy the gate.

**Anti-pattern:** inventing or cherry-picking noise, trivial stats, or “something weird” to tick the box. **Gaming this gate is a boundary breach** (same class as §6), not a successful deliverable.

If **any** of the above is not met, the implementation is considered **non-valuable** for progression: **do not extend** it with VERIFY, ALERT, or QUARANTINE until the observe layer meets this bar or the gap is explicitly recorded and resolved in [docs/OPEN_QUESTIONS.md](docs/OPEN_QUESTIONS.md) with owner agreement.

This is not a metrics dashboard requirement — it is the **meaning** test for the observe layer.

---

## 11. After the first deliverable

Only after the first deliverable is reviewed and merged:

- Add **VERIFY** and **ALERT** in small, explicit steps per [docs/MVP_ROADMAP.md](docs/MVP_ROADMAP.md).
- **QUARANTINE** only when the adapter declares a mechanism and QUARANTINE mode has been contract-reviewed.

---

## 12. Definition of success (first version)

The first implementation wave is **successful** if:

- The guard runs **outside** the protected system’s decision path and never writes to protected artifacts.
- The first deliverable meets the **Definition of success (first deliverable)** in §10 (including the four criteria and the non-vacuous observe signal), not only the bullet list above it.
- Later steps: default mode remains **OBSERVE**; escalation to VERIFY and ALERT is **explicit** and **logged**.
- Every alert and mode transition is **auditable** from the guard’s own trail.
- **No hidden authority**: if it isn’t in a contract, it doesn’t exist in code.
- Reviewers can answer “is this a second brain?” with **no** — it remains boundary integrity only.

**Violation of architecture** = any change that lets the guard decide *for* the protected system, mutate its truth layer, or enforce without contract/mode/audit.

---

## Core lines (non-negotiable)

> **The guard protects the boundary, not the decision.**

You enter an existing frame — you do not invent a new one on the fly.

> **If the guard becomes necessary for the protected system to function — the design is wrong.**

Optional is fine; invisible critical-path dependency is not.
