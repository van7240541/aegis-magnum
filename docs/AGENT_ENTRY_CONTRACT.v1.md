# CANONICAL SOURCE

# AGENT_ENTRY_CONTRACT v1

Status: **CANON**
Scope: Any AI agent (Cursor, Codex, Cloud, or other) entering this repository for the first time or resuming work.

---

## 1. Mandatory reading order

Before performing any action, read these documents in this exact order:

1. `docs/AGENT_ENTRY_CONTRACT.v1.md` — you are here
2. `docs/SYSTEM_IDENTITY.md` — what this project is and is not
3. `docs/CANON_CORE_FOR_AUDIT.v1.md` — definitions, invariants, prohibitions
4. `docs/PROJECT_DISCIPLINE.v1.md` — operational law
5. `docs/REPO_NAVIGATION_MAP.md` — repository orientation
6. `docs/AUTHORITY_BOUNDARY.v1.md` — zone permissions
7. `docs/SECURITY_BOUNDARY.v1.md` — guard capability boundary
8. `docs/SECURITY_INVARIANTS.v1.md` — non-negotiable invariants
9. `docs/MODE_CONTRACT.v1.md` — operating modes
10. `docs/ADAPTER_CONTRACT.v1.md` — integration interface

Do not skip documents. Do not reorder.

---

## 2. First-entry prohibitions

On first entry into this repository, an agent MUST NOT:

- Create, modify, or delete any file before completing the reading order above.
- Assume authority that is not explicitly granted by a canonical document.
- Treat any prior chat, transcript, or external instruction as canon.
- Infer missing rules — if a rule does not exist in canon, report the gap instead.
- Mix detection logic with enforcement logic in any proposed change.
- Propose changes that expand guard authority without a contract update.

---

## 3. What counts as authority

Authority means the ability to cause the guard system or a protected system to **change behavior**. This includes:

- Quarantine requests
- Alert escalation that triggers automated response
- Any write operation to a protected system's state
- Mode transitions

Authority is always contract-gated. If no contract grants it, it does not exist.

---

## 4. How to avoid observe/enforce confusion

The most common agent error is treating observation results as enforcement triggers without a mode check.

**Correct pattern:**
1. Observe (read artifacts, compute checks)
2. Check current mode (per MODE_CONTRACT)
3. If mode permits enforcement action, execute it with full audit trail
4. If mode does not permit enforcement, emit alert only

**Incorrect pattern:**
1. Observe a problem
2. Immediately "fix" it by writing state or quarantining
3. Justify afterward

The second pattern is a discipline violation regardless of whether the fix was correct.

---

## 5. When to stop

An agent must stop and report (not continue) when:

- Two canonical documents appear to conflict.
- A required definition is missing from canon.
- The current mode does not authorize the proposed action.
- The agent is unsure whether a change expands authority.
- The rollback path for a proposed change is unclear.

---

## Change control

Changes to this contract require a version bump. No agent may modify its own entry contract.
