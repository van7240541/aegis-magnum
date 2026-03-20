# CANONICAL SOURCE

# CHANGE_DISCIPLINE v1

Status: **CANON**
Scope: Rules for making changes to the Aegis Magnum repository and its deployed guard instances.

---

## 1. Core rule

Every change must be:

- **Scoped**: explicitly state which files, sections, or behaviors are affected.
- **Diffable**: expressible as a diff against the current state.
- **Rollbackable**: describe how to undo the change if it causes problems.
- **Non-expanding**: must not silently expand the guard's authority beyond existing contracts.

---

## 2. Change classification

### Type A — Documentation / Governance

Changes to canonical documents that do not alter guard runtime behavior.

- Examples: clarifications, new drafts, navigation map updates.
- Requires: commit, review.
- Does not require: runtime restart, deployment action.

### Type B — Observe-only logic

Changes to guard modules that affect observation, verification, or alerting but do not grant new enforcement capability.

- Examples: new invariant check, new alert condition, new artifact schema in adapter.
- Requires: commit, review, basic runtime verification.
- Does not require: contract update (unless new mode capability is introduced).

### Type C — Authority / Enforcement

Changes that expand what the guard is permitted to do (new modes, new quarantine mechanisms, new enforcement paths).

- Examples: enabling QUARANTINE for a new adapter, adding a new quarantine mechanism, any BLOCK-related work.
- Requires: contract update (version bump of relevant canonical document), explicit review, staged rollout.
- Must include: updated threat assessment, rollback plan, verification checklist.

---

## 3. Prohibited change patterns

- **Silent authority expansion**: changing guard behavior to do more without updating the contract. This is a discipline violation regardless of whether the expanded behavior is correct.
- **Undocumented configuration**: adding new config flags that alter guard behavior without documenting them in the relevant contract or adapter spec.
- **Direct production edits**: changing guard behavior on a live deployment without going through version control. Drift is a discipline violation per [PROJECT_DISCIPLINE.v1.md](PROJECT_DISCIPLINE.v1.md).
- **Removing safety checks without contract update**: disabling invariant checks, removing alert conditions, or weakening fail-closed behavior without a documented, reviewed exception.

---

## 4. Rollback requirement

Every Type B and Type C change must include a rollback path:

- **Type B**: describe how to revert the guard to its previous observation/verification behavior.
- **Type C**: describe how to revoke the expanded authority and return to the previous mode configuration.

"Rollback is not possible" is not acceptable. If true, the change must be decomposed into smaller reversible steps.

---

## 5. Review protocol

- **Type A**: self-review or peer review acceptable.
- **Type B**: peer review required. Reviewer must verify that no authority expansion occurred.
- **Type C**: owner review required. Reviewer must verify contract alignment, rollback path, and that no silent authority was introduced.

---

## 6. Drift control

The deployed guard must match the repository state:

- Before any deployment sync: check version control status. If uncommitted changes exist, stop.
- After deployment sync: verify the deployed version matches the expected commit.
- Drift (deployed state diverging from repo state) must be resolved immediately by returning to the repo-tracked state.

---

## Change control

Changes to this discipline document require a version bump if they alter the classification system, review requirements, or rollback obligations.
