# DRAFT

# ADAPTER_RESEARCH v1

**Status:** DRAFT — research and open questions for how a concrete adapter maps a protected system onto Aegis guard capabilities. **Not** binding canon; see [ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md) for the draft interface summary.

---

## Purpose

Capture **non-final** exploration:

- Which artifact types and paths are observable without coupling to protected runtime code.
- How quarantine or emergency-stop might be requested **by the protected system’s existing mechanism** (if any).
- What invariants are **verify-only** vs need product-owner approval.

---

## Research checklist (examples)

- [ ] Process identity and health signals (PID file, systemd, lock files).
- [ ] Append-only or rotated logs; schema stability.
- [ ] Configuration drift detection without storing secret contents in guard config.
- [ ] Independent alert channel vs operational bot identity.
- [ ] Failure modes if guard is down (protected system must still run).

---

## Out of scope for this draft

- Execution paths, domain-specific privileged APIs, or “executor implementation.”
- **Raw-intent semantics** or any path from observed data to **external effect**.
- **Decision-quality** or **strategy** evaluation — not an adapter concern.
- Importing **host-product vocabulary** (e.g. internal layer or gate names) into Aegis as if it were global canon; use **neutral** terms here and map in host-specific notes outside this draft if needed.
- Concrete host file paths as **requirements** in this repo (belong in deployment-specific docs).

---

## Next steps

Promote findings into versioned **CANON** only through review with [SYSTEM_SECURITY_MODEL.v1.md](SYSTEM_SECURITY_MODEL.v1.md) and [SECURITY_BOUNDARY_ALIGNMENT.md](SECURITY_BOUNDARY_ALIGNMENT.md).
