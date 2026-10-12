---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/web-auth.ts"
    }
  ]
}
---

# Web session

Source-bound browser identity and separately checked target and allowed scope. Activity window, absolute expiry and revocation are distinct.

## Information kept

- **Identity** — Stable addressable identity.
- **Principal** — The principal of this web session, retained or disclosed with the object.
- **Authentication source** — The exact retained source kind (credential or web_authenticator) and source ID belonging to its Principal.
- **Target** — The retained target kind and target identifiers; fixed scope is not expanded by navigation or renewal.
- **Allowed scope** — Permitted data and management scope, never expanded during revalidation.
- **Entry** — The entry of this web session, retained or disclosed with the object.
- **Created at** — Creation time retained with history.
- **Activity at** — The activity at of this web session, retained or disclosed with the object.
- **Expires at** — The expires at of this web session, retained or disclosed with the object.
- **Absolute expiry** — The absolute expiry of this web session, retained or disclosed with the object.
- **Version** — Current concurrency version, advanced with a successful change.
- **Revoked at** — Revocation time, absent while the source remains active.

## States

### Active

Current, without archival, deletion or revocation.

### Expired

Past its validity boundary as computed from the retained expiry and current time; expiry is not an authored state-changing write.

### Revoked

Revoked and no longer usable as a current source.
