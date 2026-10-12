---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/access.ts"
    }
  ]
}
---

# Credential

Nonsecret credential metadata. The secret is delivered only through private state and trusted origins, never as an ordinary displayed fact.

## Information kept

- **Identity** — Stable addressable identity.
- **Principal** — The principal of this credential, retained or disclosed with the object.
- **Fingerprint** — Nonsecret credential fingerprint, never its bearer secret.
- **Device name** — Optional saved device label returned in nonsecret management metadata; an ordinary newly joined identity defaults to no label.
- **Revocation reason** — Saved reason such as owner_revoke, participant_rotation or participant_full_recovery; absent for an active source.
- **Version** — Computed management concurrency version: 1 while active and 2 after revocation.
- **Created at** — Creation time retained with history.
- **Last used at** — The last used at of this credential, retained or disclosed with the object.
- **Revoked at** — Revocation time, absent while the source remains active.

## States

### Active

Current, without archival, deletion or revocation.

### Revoked

Revoked and no longer usable as a current source.
