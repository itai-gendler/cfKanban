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
      "entity": "project",
      "verb": "contains",
      "cardinality": "one-to-many"
    },
    {
      "entity": "workspace-administrator-grant",
      "verb": "contains",
      "cardinality": "one-to-many"
    }
  ]
}
---

# Workspace

Project container retaining metadata and archival history; aggregate trends cover all its active Projects.

## Information kept

- **Identity** — Stable addressable identity.
- **Name** — The name of this workspace, retained or disclosed with the object.
- **Description** — The description of this workspace, retained or disclosed with the object.
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
