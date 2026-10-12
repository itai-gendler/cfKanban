---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/passkeys.ts"
    }
  ]
}
---

# Passkey

Registered authenticator and nonsecret inventory with revocation history.

## Information kept

- **Identity** — Stable addressable identity.
- **Principal** — The principal of this passkey, retained or disclosed with the object.
- **Authenticator description** — The authenticator description of this passkey, retained or disclosed with the object.
- **Created at** — Creation time retained with history.
- **Last used at** — The last used at of this passkey, retained or disclosed with the object.
- **Version** — Current concurrency version, advanced with a successful change.
- **Revoked at** — Revocation time, absent while the source remains active.

## States

### Active

Current, without archival, deletion or revocation.

### Revoked

Revoked and no longer usable as a current source.
