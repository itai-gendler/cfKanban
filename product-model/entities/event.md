---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/events.ts"
    }
  ]
}
---

# Event

User-visible domain activity and Owner audit history of actual actor, source, operation, subject and payload.

## Information kept

- **Identity** — Stable addressable identity.
- **Sequence** — Stable sequence within its event stream.
- **Stream** — The stream of this event, retained or disclosed with the object.
- **Operation** — The operation of this event, retained or disclosed with the object.
- **Actor principal** — The actor principal of this event, retained or disclosed with the object.
- **Actor credential** — The actor credential of this event, retained or disclosed with the object.
- **Authorized via** — The authorized via of this event, retained or disclosed with the object.
- **Workspace** — The workspace of this event, retained or disclosed with the object.
- **Project** — The project of this event, retained or disclosed with the object.
- **Subject** — The subject of this event, retained or disclosed with the object.
- **Payload** — The payload of this event, retained or disclosed with the object.
- **Created at** — Creation time retained with history.
