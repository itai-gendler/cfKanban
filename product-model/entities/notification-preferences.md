---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/notifications.ts"
    }
  ]
}
---

# Notification preferences

Identity reception setting and receive-after boundary. Reenable resets that boundary and keeps history.

## Information kept

- **Principal** — The principal of this notification preferences, retained or disclosed with the object.
- **Enabled** — The enabled of this notification preferences, retained or disclosed with the object.
- **Receive after** — Reception start boundary reset on off-to-on.
- **Version** — Current concurrency version, advanced with a successful change.

## States

### Enabled

Reception enabled for eligible unseen notices after the start boundary.

### Disabled

Reception disabled while history remains.
