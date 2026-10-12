---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/comments.ts"
    }
  ]
}
---

# Comment

Append-only ordinary comment or reply, separately soft-deleted and restored.

## Information kept

- **Identity** — Stable addressable identity.
- **Body** — The body of this comment, retained or disclosed with the object.
- **Author** — The author of this comment, retained or disclosed with the object.
- **Created at** — Creation time retained with history.
- **Reply target** — The reply target of this comment, retained or disclosed with the object.
- **Version** — Current concurrency version, advanced with a successful change.
- **Deleted at** — Soft deletion time, absent while active.
- **Deleted by** — Stable identity that soft-deleted the object.

## States

### Active

Current, without archival, deletion or revocation.

### Deleted

Soft-deleted with historical relations retained.
