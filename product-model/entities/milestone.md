---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/milestones.ts"
    }
  ],
  "relations": [
    {
      "entity": "issue",
      "verb": "contains",
      "cardinality": "one-to-many"
    }
  ]
}
---

# Milestone

Optional same-Project target; closing it does not complete its work items. Progress distinguishes Done, Canceled and unfinished.

## Information kept

- **Identity** — Stable addressable identity.
- **Title** — The title of this milestone, retained or disclosed with the object.
- **Description** — The description of this milestone, retained or disclosed with the object.
- **Due date** — The due date of this milestone, retained or disclosed with the object.
- **Status** — Current fixed workflow or milestone status.
- **Version** — Current concurrency version, advanced with a successful change.
- **Progress** — Derived counts excluding deleted work items and separating Done, Canceled and unfinished.

## States

### Open

Open milestone.

### Closed

Closed milestone, still readable and associable without advancing work.
