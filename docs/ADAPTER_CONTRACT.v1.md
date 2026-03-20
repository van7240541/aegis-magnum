# DRAFT

# ADAPTER_CONTRACT v1

**Status:** DRAFT — interface expectations for connecting an Aegis guard core to a **protected system**. Does **not** specify APIs, languages, or runtime code. Does **not** authorize execution or bypass [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md).

---

## 1. Role

The guard core is **domain-agnostic** and must **not** assume trading, finance, or any single industry. **Execution mapping** (what counts as host output, validation boundary, execution component, external target) is **adapter-defined** and **host-specific** — it does **not** live in universal canon.

The adapter describes:

- What to observe (artifact locations, formats, schemas — as configuration).
- What **integrity / structural** checks to run (definitions and severities owned by the product or agreed with operators) — **not** domain merit, PnL, or “quality” of business outcomes.
- How a **quarantine or emergency restriction request** is formulated **if** the protected system exposes such a mechanism (request only; protected system remains authoritative).

**Host vocabulary is local:** layer names, state machines, artifact filenames, and domain terms (**including** those of any **example** host such as Opus Magnum) belong in **adapter config and host docs**, not in universal Aegis core or canon text. The core treats adapter-supplied fields as **opaque labels** unless a cross-reference is documented in [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md) for that deployment.

---

## 2. Adapter anti-drift (non-negotiable)

Adapters are the **highest-risk place** for silent evolution into a second decision layer: “helpful” interpretation becomes scoring, then filtering, then policy. The following rules apply **without exception**.

**Adapters MUST NOT** perform **domain-level** evaluation, scoring, ranking, or decision-making under any circumstances.

**Adapters MAY** transform, validate, and **map** (structural shape, schema, field routing) — but **MUST NOT** interpret the **merit**, **correctness**, **optimality**, or **desirability** of host outputs in any business, safety, financial, or strategic sense.

**Allowed:** syntactic validation, schema conformance, integrity checks, joins, hashes, presence/absence of fields, and other checks that do **not** encode “is this a good/bad outcome for the domain.” **Forbidden:** “quality gates,” “helpfulness” filters, or thresholds whose **meaning** depends on domain judgment unless that judgment is **only** reproducing a **numeric rule already published by the host** (mechanical comparison), not invented in the adapter.

Violation of this section is a **boundary breach** — same class as [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md) §3 — not an implementation shortcut.

---

## 3. Required capability areas

1. **Discovery** — name/version of protected system; optional process and service identifiers (patterns, not hardcoded paths in universal docs).
2. **Artifact sources** — observable inputs (e.g. structured logs), growth expectations, read-only access assumptions.
3. **Critical files** — configuration or policy files whose change should raise alerts; hash/mtime strategy.
4. **Invariants** — ID, description, check method, severity; references to **that host’s** product canon where applicable.
5. **Process specification** — expected runtime identity; health hints.
6. **Boundary actions** — **if** supported: mechanism for **requesting** emergency restriction through the protected system’s **own** operator path; **no** direct execution from the guard.
7. **Execution boundary (if applicable)** — how this host exposes **validated execution payloads** vs **unvalidated host output** — **mapping is adapter-defined**; core must not hardcode semantics.

---

## 4. Prohibitions

- No embedding of **secrets** in adapter definitions checked into canon (use indirection to secret stores).
- No submission of **unvalidated host output** or **raw execution requests** to execution endpoints from the adapter — [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md).
- No **decision-quality** or **domain optimality** interpretation disguised as invariant checks.
- No requirement that the protected system **import** guard code.
- No leakage of **host-specific** vocabulary into **universal** Aegis canon files — keep those strings in adapter-local configuration.

---

## 5. References

- [SYSTEM_SECURITY_MODEL.v1.md](SYSTEM_SECURITY_MODEL.v1.md) — trust boundaries.
- [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md) — relation to a host’s `SECURITY_BOUNDARY` / invariants (per deployment).
- [FUTURE_EXECUTION_SECURITY.v1.md](FUTURE_EXECUTION_SECURITY.v1.md) — universal execution risk class.
- [ADAPTER_RESEARCH.v1.md](ADAPTER_RESEARCH.v1.md) — open research notes.

---

**Version:** v1 (draft)
