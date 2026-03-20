# CANONICAL SOURCE

# DOCS_MAINTENANCE — Document Maintenance Policy

Status: **CANON**
Purpose: Ensure canonical documents stay in sync with the guard system's codebase, contracts, and adapter implementations.

---

## Maintained documents (update together when affected)

| Document | Role |
|----------|------|
| **REPO_NAVIGATION_MAP.md** | 2-minute orientation: layout, entry points, reading path |
| **CANON_CORE_FOR_AUDIT.v1.md** | Definitions, invariants, prohibitions, precedence |
| **SYSTEM_IDENTITY.md** | What the project is and is not |

When in doubt, check all three after a structural change.

---

## Triggers: when to update

### Guard core modules

- Add, remove, or rename core modules (engine, modes, scheduler, policy engine, etc.)
- Change the responsibility of an existing module.

Update: REPO_NAVIGATION_MAP, INITIAL_MODULE_MAP (if still in bootstrap phase).

### Adapters

- Add a new adapter for a protected system.
- Change an existing adapter's interface or quarantine mechanism.
- Remove an adapter.

Update: REPO_NAVIGATION_MAP, ADAPTER_CONTRACT (if interface changes).

### Contracts and invariants

- Add, remove, or modify a security invariant.
- Add or modify a mode definition.
- Change quarantine semantics.
- Change authority boundaries.

Update: CANON_CORE_FOR_AUDIT, and the specific contract document. Verify SECURITY_INVARIANTS and SECURITY_BOUNDARY remain aligned.

### Repository structure

- Add or remove top-level directories.
- Rename or relocate canonical documents.
- Change the entry point or reading path.

Update: REPO_NAVIGATION_MAP, AGENT_ENTRY_CONTRACT (if reading order changes).

### New canonical document

- Any new document with status CANONICAL SOURCE must be added to:
  - REPO_NAVIGATION_MAP (section 4, "where to find what")
  - CANON_CORE_FOR_AUDIT (if it defines invariants or prohibitions)
  - AGENT_ENTRY_CONTRACT (if it should be in the mandatory reading order)

---

## Who updates

- **Developers and AI agents**: When making a change that matches any trigger above, update the relevant documents in the same commit or immediately after.
- **Reviewers**: In PRs that touch contracts, modes, adapters, or repository structure, check that the maintained documents were updated.

---

## Checklist (before merge)

If your change touched any of:

- `core/` modules
- `adapters/` (new or modified)
- `contracts/` or `docs/` canonical documents
- Repository top-level structure
- Mode definitions, invariant definitions, quarantine semantics

Then confirm:

- [ ] REPO_NAVIGATION_MAP still accurate
- [ ] CANON_CORE_FOR_AUDIT invariants and prohibitions still accurate
- [ ] SYSTEM_IDENTITY still accurate (if scope changed)
- [ ] AGENT_ENTRY_CONTRACT reading order still correct
- [ ] Cross-references between documents still valid
