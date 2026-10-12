---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/labels.ts"
    }
  ]
}
---

# Label

Individually addressable Project label definition. Deletion keeps its old associations and their count.

## Information kept

- **Identity** — Stable addressable identity.
- **Name** — The name of this label, retained or disclosed with the object.
- **Marker** — The marker of this label, retained or disclosed with the object.
- **Version** — Current concurrency version, advanced with a successful change.
- **Deleted at** — Soft deletion time, absent while active.
- **Deleted by** — Stable identity that soft-deleted the object.

## States

### Active

Current, without archival, deletion or revocation.

### Deleted

Soft-deleted with historical relations retained.
