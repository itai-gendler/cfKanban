---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/issues.ts"
    }
  ],
  "relations": [
    {
      "entity": "comment",
      "verb": "has",
      "cardinality": "one-to-many"
    },
    {
      "entity": "completion-record",
      "verb": "has",
      "cardinality": "one-to-many"
    },
    {
      "entity": "attachment",
      "verb": "has",
      "cardinality": "one-to-many"
    },
    {
      "entity": "label",
      "verb": "has",
      "cardinality": "many-to-many"
    },
    {
      "entity": "relation",
      "verb": "is-source-of",
      "cardinality": "one-to-many"
    },
    {
      "entity": "relation",
      "verb": "is-target-of",
      "cardinality": "one-to-many"
    }
  ]
}
---

# Issue

Individually identified work item. Status, assignee, manual blocking, labels, milestone and soft deletion are distinct facts. Visible blocking is derived from current visible neighbours.

## Information kept

- **Identity** — Stable addressable identity.
- **Identifier** — The identifier of this issue, retained or disclosed with the object.
- **Title** — The title of this issue, retained or disclosed with the object.
- **Body** — The body of this issue, retained or disclosed with the object.
- **Status** — Current fixed workflow or milestone status.
- **Priority** — The priority of this issue, retained or disclosed with the object.
- **Assignee** — The assignee of this issue, retained or disclosed with the object.
- **Manual block reason** — The manual block reason of this issue, retained or disclosed with the object.
- **Visible blocking** — Manual reason or visible non-Done blocker; Canceled still blocks.
- **Labels** — The labels of this issue, retained or disclosed with the object.
- **Milestone** — The milestone of this issue, retained or disclosed with the object.
- **Created at** — Creation time retained with history.
- **Updated at** — Most recent persisted update time.
- **Version** — Current concurrency version, advanced with a successful change.
- **Deleted at** — Soft deletion time, absent while active.
- **Deleted by** — Stable identity that soft-deleted the object.

## States

### Backlog

Not yet in the executable Todo queue.

### Todo

Pending work eligible for explicitly selected candidate queues.

### In Progress

Work currently in progress.

### Done

Entered through completion with its evidence record.

### Canceled

Canceled, still completable and still able to block a neighbour.
