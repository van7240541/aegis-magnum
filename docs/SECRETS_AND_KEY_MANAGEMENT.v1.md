# CANONICAL SOURCE

# SECRETS_AND_KEY_MANAGEMENT v1

**Scope:** Policy for classifying, storing, rotating, and revoking secrets used in environments where Aegis or a protected system may operate. **No secret values** belong in this repository.

---

## 1. Secret types (non-exhaustive)

| Type | Typical use | Risk |
|------|-------------|------|
| **SSH host keys / client keys** | Server access | Full host compromise if leaked |
| **Git / CI tokens** | Repository, pipelines | Code and workflow takeover |
| **Cloud / VPS panel** | Infrastructure control | Wide blast radius |
| **Messaging / bot tokens** | Alerts or ops automation | Impersonation, data exfiltration |
| **Execution / privileged API keys** | Automated external action | Financial, operational, or legal risk depending on domain |
| **TLS private keys** | Service identity | MITM, impersonation |
| **Signing / webhook secrets** | Callback authentication | Forged events |

---

## 2. Storage rules

1. **Never** commit secrets to git (including `.env` tracked in repo, “temporary” comments, fixtures with real tokens).
2. Prefer **environment-specific** secret stores: encrypted files outside VCS, OS keyrings, or a managed secret manager — exact mechanism is operational, not canon here.
3. **Separate** development, staging, and production material; do not reuse production keys in dev.
4. **Minimum exposure:** only processes that require a secret receive it; avoid a single file containing all roles’ credentials on one host “for convenience.”
5. **Documentation** may describe *where* classes of secrets live (e.g. “per-service env file readable only by service user”), not the values.

---

## 3. Least privilege

- Each key or token is issued for **one primary purpose**; split credentials rather than one super-token.
- Scope API keys to required permissions only (read-only vs privileged action, IP allowlists where supported).
- Human access to production secrets is **separate** from automated service accounts.

---

## 4. Rotation policy

| Trigger | Action |
|---------|--------|
| Scheduled interval | Rotate high-value keys per organizational policy (e.g. 90 days or per provider recommendation) |
| Personnel change | Revoke and replace keys accessible by departing operators |
| Suspected leak | Immediate revocation — [INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md](INCIDENT_RESPONSE_AND_KEY_COMPROMISE.v1.md) |
| Provider incident | Follow provider advisory; rotate if advised |

Rotation must be **documented** (what was rotated, when, by whom — in operational ticketing, not in git).

---

## 5. Revocation procedure

1. **Identify** the compromised or obsolete credential in the inventory.
2. **Invalidate** at the issuer (GitHub, cloud, exchange, bot API) first.
3. **Deploy** replacement credentials to affected systems.
4. **Verify** services healthy with new material; monitor for auth errors.
5. **Record** the event (incident log).

---

## 6. Inventory

Maintain a living inventory (location may be outside this repo: spreadsheet, vault metadata) listing:

- Secret identifier (type + purpose, not the value)
- Owner / team
- Rotation due date
- Scope (which hosts or services)

---

## 7. Relationship to Aegis

The guard layer must **not** embed secrets in canon documents. Adapter implementations that read paths to secret stores must treat those paths as configuration, not hardcoded credentials — see [ADAPTER_CONTRACT.v1.md](ADAPTER_CONTRACT.v1.md) (draft).

---

**Version:** v1
