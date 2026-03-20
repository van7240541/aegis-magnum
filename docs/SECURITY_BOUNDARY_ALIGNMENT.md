# CANONICAL SOURCE

# SECURITY_BOUNDARY_ALIGNMENT — Aegis and a host product (e.g. Opus Magnum)

**Scope:** Explains how **Aegis Magnum** (this export) relates to a **protected system** that maintains its own security canon — for example a repository that defines `SECURITY_BOUNDARY` and `SECURITY_INVARIANTS` for application-layer guard behavior. **Opus Magnum** is used here as a **concrete example** host; the same alignment pattern applies to **any** protected system with analogous contracts.

---

## 1. Two levels

| Level | Owns | Examples |
|-------|------|----------|
| **Protected system (example: Opus Magnum)** | Decision authority, permission/risk semantics, runtime artifact truth, domain/guard modes as defined **in that repo** | `SECURITY_BOUNDARY`, `SECURITY_INVARIANTS`, pipeline invariants |
| **Aegis Magnum (this tree)** | Trust-chain security architecture: secrets, hosts, access, future execution containment, IR; optional guard implementation **outside** decision path | `SYSTEM_SECURITY_MODEL`, hardening baselines, adapter drafts |

These levels are **complementary**. Neither replaces the other.

---

## 2. What the host product (e.g. Opus) controls

- **Decision** and **interpretation** of domain data into internal outcomes.
- **Permission** and **gate** semantics as defined in that product’s canon.
- **What** counts as violation of runtime invariants (`SECURITY_INVARIANTS`).

Aegis documentation **does not** redefine those semantics.

---

## 3. What Aegis adds

- **Infrastructure and operations security**: how humans, keys, servers, and integrations are managed — [SYSTEM_SECURITY_MODEL.v1.md](SYSTEM_SECURITY_MODEL.v1.md).
- **Guard-friendly** boundaries when a separate process observes the protected system: no hidden authority, removable guard, fail-closed automation — aligned in spirit with external guard rules in the host’s `SECURITY_BOUNDARY`, but expressed here in **system-agnostic** language.

---

## 4. Explicit non-replacement

- Aegis **does not replace** the host product’s **`SECURITY_BOUNDARY`** or **`SECURITY_INVARIANTS`**. Those remain the binding application contracts **in that repository**.
- Aegis **does not** grant itself decision authority over the protected system.
- If both are deployed, **precedence** for runtime behavior is: **host product canon first** for decision and artifact authority; **Aegis root model** for how this export’s security contour is interpreted — resolve conflicts by explicit human review, not by silent merge.

---

## 5. Synchronization

When updating either side:

- Changes to **decision authority** or **artifact write rules** → host repo.
- Changes to **key management**, **VPS posture**, **incident response** for the chain of trust → Aegis export (this tree) and operational runbooks.

---

## 6. Removability

The protected system must remain operable **without** Aegis. If Aegis becomes a hard dependency for core operation, that is a **design error** relative to [SYSTEM_SECURITY_MODEL.v1.md](SYSTEM_SECURITY_MODEL.v1.md) and the host’s external-guard principles.

---

**Version:** v1
