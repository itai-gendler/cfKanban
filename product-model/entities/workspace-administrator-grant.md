---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/scoped-administrators.ts"
    }
  ]
}
---

# Workspace administrator grant

Workspace management source with generation-sensitive revocation and regranting.

## Information kept

- **Identity** — Stable addressable identity.
- **Principal** — The principal of this workspace administrator grant, retained or disclosed with the object.
- **Workspace** — The workspace of this workspace administrator grant, retained or disclosed with the object.
- **Version** — Current concurrency version, advanced with a successful change.
- **Generation** — Current management-source generation; old generations are not revived.
- **Granted at** — Time of this grant.
- **Granted by** — Administrator granting actor retained in the atomic security Event for the operation, not a separate row column or ordinary list field.
- **Revoked at** — Revocation time, absent while the source remains active.
- **Revoked by** — Stable revoking identity.

## States

### Active

Current, without archival, deletion or revocation.

### Revoked

Revoked and no longer usable as a current source.
