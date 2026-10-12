---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/notifications.ts"
    }
  ],
  "relations": [
    {
      "entity": "notification-acknowledgement",
      "verb": "has",
      "cardinality": "one-to-many"
    }
  ]
}
---

# Notification

Published immutable notice with expiry calculated from time and separately persisted withdrawal.

## Information kept

- **Identity** — Stable addressable identity.
- **Title** — The title of this notification, retained or disclosed with the object.
- **Body** — The body of this notification, retained or disclosed with the object.
- **Publisher** — The publisher of this notification, retained or disclosed with the object.
- **Published at** — The published at of this notification, retained or disclosed with the object.
- **Expires at** — The expires at of this notification, retained or disclosed with the object.
- **Withdrawn at** — The withdrawn at of this notification, retained or disclosed with the object.
- **Version** — Current concurrency version, advanced with a successful change.
- **Visible status** — Status calculated from expiry and withdrawal, without a timer-write assumption.

## States

### Active

Current, without archival, deletion or revocation.

### Expired

Past its validity boundary as computed from the retained expiry and current time; expiry is not an authored state-changing write.

### Withdrawn

Withdrawn notice with history retained.
