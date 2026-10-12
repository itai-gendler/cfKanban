---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/relations.ts"
    }
  ]
}
---

# Relation

Directed relationship between two explicit work items. Only related normalizes endpoints; parent must remain acyclic.

## Information kept

- **Identity** — Stable addressable identity.
- **Kind** — The kind of this relation, retained or disclosed with the object.
- **Source** — The source of this relation, retained or disclosed with the object.
- **Target** — The target of this relation, retained or disclosed with the object.
- **Source version** — The source version of this relation, retained or disclosed with the object.
- **Target version** — The target version of this relation, retained or disclosed with the object.
- **Version** — Current concurrency version, advanced with a successful change.
- **Deleted at** — Soft deletion time, absent while active.
- **Deleted by** — Stable identity that soft-deleted the object.

## States

### Active

Current, without archival, deletion or revocation.

### Deleted

Soft-deleted with historical relations retained.
