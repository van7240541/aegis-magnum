# CANONICAL SOURCE

# COLLABORATOR_HANDOFF — Human entry

**Scope:** Operational onboarding for human engineers. Binds behavior with [docs/SYSTEM_SECURITY_MODEL.v1.md](docs/SYSTEM_SECURITY_MODEL.v1.md); does not replace per-document canon.

---

## 1. Mission

Build **Aegis Magnum** as:

1. A **full security contour** — trust chain, secrets, host posture, incident response, future execution containment — per the canon in `docs/`.
2. An optional **external guard** that attaches **outside** a protected system, observes and verifies boundary health, alerts operators, and — only under explicit contract — may request boundary restriction through mechanisms the protected system already owns.

You are **not** building a feature inside someone else’s runtime roadmap as if you owned their decision stack. You are building a **separate product** whose first deliverable is **documentation + OBSERVE-only guard skeleton** when code starts — see [docs/MVP_ROADMAP.md](docs/MVP_ROADMAP.md) Stage 0–1.

**Universal vs host-specific:** Do **not** design Aegis as an **Opus-only** (or any single-product-only) security layer. The **core** and **canon** stay **domain-neutral** and reusable; anything that names a specific host’s layers, artifacts, or business rules belongs in **adapters** and **non-canonical** deployment docs — not in universal Aegis text. **Opus Magnum** is one **example** protected system, not the definition of what Aegis is.

---

## 2. Your role in this system

You are **not** extending any protected system’s core application or decision pipeline as an insider.

You **are** designing:

- **Security architecture** (documented here) that survives partial compromise — [docs/SYSTEM_SECURITY_MODEL.v1.md](docs/SYSTEM_SECURITY_MODEL.v1.md).
- An **external** guard that: observes boundary signals; verifies against contracts and adapter-defined checks; alerts; requests quarantine **only** via adapter-described, protected-system-owned paths.

You **do not** own:

- Decision logic, risk **computation**, permission semantics, or execution authority inside the protected system.

You **are** responsible for:

- Guard architecture (when coding), adapter boundaries, guard-local auditability, and **no hidden authority** — [docs/SECURITY_BOUNDARY_ALIGNMENT.md](docs/SECURITY_BOUNDARY_ALIGNMENT.md).

---

## 3. Non-goals

- A second decision engine or automation layer that **performs external action** or domain decisions **for** the protected system.
- Rewriting protected artifacts or configuration from the guard.
- Coupling that **requires** the protected system to import guard code.
- **Executor implementation**, domain-specific execution plumbing, or passing **unvalidated host output** straight to execution — [docs/FUTURE_EXECUTION_SECURITY.v1.md](docs/FUTURE_EXECUTION_SECURITY.v1.md).
- Encoding **one host’s** vocabulary or file layout as **universal** Aegis canon (use adapters).

---

## 4. Architectural boundary

| Zone | Protected system | Aegis |
|------|------------------|--------|
| Decision / permission / risk | **Owns authority** | No participation |
| Host product `SECURITY_BOUNDARY` / invariants | **Owns** application canon | **Does not replace** — see [docs/SECURITY_BOUNDARY_ALIGNMENT.md](docs/SECURITY_BOUNDARY_ALIGNMENT.md) |
| Artifacts | **Owns writes** | Read-only observation unless explicitly contracted |
| Secrets / SSH / firewall | Shared operational reality | **Documented** in Aegis canon; operators execute |

---

## 5. Allowed work

- **Canon**: extend or patch `docs/*.md` with review; keep [docs/SYSTEM_SECURITY_MODEL.v1.md](docs/SYSTEM_SECURITY_MODEL.v1.md) coherent.
- **Guard code** (when approved): core shell, OBSERVE-first, adapter stub per [docs/ADAPTER_CONTRACT.v1.md](docs/ADAPTER_CONTRACT.v1.md) (draft), guard audit sink, channels that do not imply execution authority.
- **Operations alignment**: map [docs/SECRETS_AND_KEY_MANAGEMENT.v1.md](docs/SECRETS_AND_KEY_MANAGEMENT.v1.md) and [docs/SERVER_HARDENING_BASELINE.v1.md](docs/SERVER_HARDENING_BASELINE.v1.md) to your environment in **non-canonical** runbooks (not in this repo’s canon text).

**Scope expansion** requires explicit doc update and review — not silent README edits.

---

## 6. Forbidden work

- Modify **protected runtime** (vendor tree, live pipeline, host secrets) to “make Aegis work” without controlled change process.
- **Hidden authority**: side effects not in a versioned contract.
- Inject or rewrite **intents**, **decisions**, or **events** in protected streams.
- **BLOCK** / execution interposition without a **future** product-specific enforcement contract — not in v1.
- **Gaming** the OBSERVE success criteria (§10).

**Violating any of the above is a boundary breach, not an implementation mistake.**

---

## 7. If you are unsure

**Default:** **no action** on the Aegis side that could expand authority, touch protected runtime, or introduce enforcement — until the ambiguity is resolved.

1. **Do not implement** the risky part.
2. **Document** the question in your **project tracker** or [docs/ADAPTER_RESEARCH.v1.md](docs/ADAPTER_RESEARCH.v1.md) (draft).
3. **Proceed** only after alignment with [docs/SYSTEM_SECURITY_MODEL.v1.md](docs/SYSTEM_SECURITY_MODEL.v1.md) and [docs/SECURITY_BOUNDARY_ALIGNMENT.md](docs/SECURITY_BOUNDARY_ALIGNMENT.md).

Uncertainty is **not** a license to “ship something reasonable.” The protected system may keep running; Aegis must not fill gaps with improvised power.

---

## 8. What a bad implementation looks like

- Guard **modifies** protected decision or audit artifacts.
- Guard introduces **competing** decision or execution logic.
- Guard **silently** blocks or rewrites execution without operator visibility.
- Guard becomes **required** for protected system operation.
- **All keys** on one host “for convenience”; one process with **secrets + execution** without split.

Any of the above is a **design violation**.

---

## 9. Required reading order

Complete [README.md](README.md) and this handoff first, then read **in order**:

1. [docs/SYSTEM_SECURITY_MODEL.v1.md](docs/SYSTEM_SECURITY_MODEL.v1.md)
2. [docs/SECURITY_BOUNDARY_ALIGNMENT.md](docs/SECURITY_BOUNDARY_ALIGNMENT.md)
3. [docs/FUTURE_EXECUTION_SECURITY.v1.md](docs/FUTURE_EXECUTION_SECURITY.v1.md)
4. [docs/SECRETS_AND_KEY_MANAGEMENT.v1.md](docs/SECRETS_AND_KEY_MANAGEMENT.v1.md)
5. [docs/SERVER_HARDENING_BASELINE.v1.md](docs/SERVER_HARDENING_BASELINE.v1.md)
6. [docs/INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md](docs/INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md)
7. [docs/ADAPTER_CONTRACT.v1.md](docs/ADAPTER_CONTRACT.v1.md)
8. [docs/ADAPTER_RESEARCH.v1.md](docs/ADAPTER_RESEARCH.v1.md)
9. [docs/MVP_ROADMAP.md](docs/MVP_ROADMAP.md)
10. [docs/REPO_NAVIGATION_MAP.md](docs/REPO_NAVIGATION_MAP.md)

---

## 10. First deliverable (strict)

The first deliverable is **observe-only architecture work**: canon-respecting **documentation** plus, when code starts, a **minimal guard skeleton** — **not** enforcement, **not** quarantine, **not** BLOCK.

Minimal guard skeleton (when implemented):

- **OBSERVE only**; structured audit events in guard’s sink; **no** change to protected behavior; **fully disable-able**; demonstrates adapter stub **without** enforcement or quarantine.

### Definition of success

Same gate as before: **reproducible** audit artifact; **zero** behavior change when off; **disable** without runtime impact; **at least one valid non-vacuous observe signal** (reproducible, non-obvious, structural or stable pattern — **changes understanding**). Otherwise **do not extend** to VERIFY/ALERT/QUARANTINE until resolved in tracker with owner agreement.

---

## 11. After the first deliverable

Per [docs/MVP_ROADMAP.md](docs/MVP_ROADMAP.md): VERIFY + ALERT in steps; QUARANTINE only with explicit adapter mechanism and review.

---

## 12. Definition of success (first wave)

- Guard outside decision path; meets §10; **auditable**; **no hidden authority**; not a second brain.
- **Security contour** (Stage 0) not ignored in real deployments.

**Violation** = guard decides *for* protected system, mutates truth layer, or enforcement without contract.

---

## Core lines

> **The guard protects the boundary, not the decision.**

> **If the guard becomes necessary for the protected system to function — the design is wrong.**
