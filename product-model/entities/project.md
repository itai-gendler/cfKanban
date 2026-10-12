---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/containers.ts"
    }
  ],
  "relations": [
    {
      "entity": "issue",
      "verb": "contains",
      "cardinality": "one-to-many"
    },
    {
      "entity": "label",
      "verb": "contains",
      "cardinality": "one-to-many"
    },
    {
      "entity": "milestone",
      "verb": "contains",
      "cardinality": "one-to-many"
    },
    {
      "entity": "project-status-name",
      "verb": "contains",
      "cardinality": "one-to-many"
    },
    {
      "entity": "project-grant",
      "verb": "contains",
      "cardinality": "one-to-many"
    },
    {
      "entity": "project-administrator-grant",
      "verb": "contains",
      "cardinality": "one-to-many"
    },
    {
      "entity": "public-join-policy",
      "verb": "has",
      "cardinality": "one-to-one"
    }
  ]
}
---

# Project

The shared subject of Board and List with metadata, archival history and derived trends.

## Information kept

- **Identity** — Stable addressable identity.
- **Name** — The name of this project, retained or disclosed with the object.
- **Context** — The context of this project, retained or disclosed with the object.
- **Created at** — Creation time retained with history.
- **Updated at** — Most recent persisted update time.
- **Version** — Current concurrency version, advanced with a successful change.
- **Archived at** — Archival time, absent while active.
- **Archived by** — Stable identity that archived the object.
- **Trend history** — UTC historical daily values; unknown history is null and the current day can be partial.
- **Trend coverage** — Known historical coverage and current-day partial status.

## States

### Active

Current, without archival, deletion or revocation.

### Archived

Archived with history retained; ordinary active access and restoration differ.
