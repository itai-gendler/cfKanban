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

# Completion record

Immutable completion evidence supplied by the caller, including defaults. Verification records a claim and never means the Product ran that verification.

## Information kept

- **Identity** — Stable addressable identity.
- **Author** — The author of this completion record, retained or disclosed with the object.
- **Created at** — Creation time retained with history.
- **Summary** — The summary of this completion record, retained or disclosed with the object.
- **Verification** — Supplied verification description and defaults; not execution evidence.
- **Artifacts** — The artifacts of this completion record, retained or disclosed with the object.
- **Follow-ups** — The follow-ups of this completion record, retained or disclosed with the object.
