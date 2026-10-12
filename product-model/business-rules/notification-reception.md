---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "notification"
    },
    {
      "type": "entity",
      "id": "notification-acknowledgement"
    },
    {
      "type": "entity",
      "id": "notification-preferences"
    },
    {
      "type": "entity",
      "id": "principal"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/notifications.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/notification-pending-cache.ts"
    }
  ]
}
---

# pending 过滤与历史读取分开

Pending reminders exclude the publisher’s own notices, acknowledged, withdrawn and expired notices and notices before the identity’s receive-after boundary. Disabled preferences yield an empty pending page. Personal history still includes notices from other publishers before joining, while reception was disabled, or after acknowledgement, expiry or withdrawal.
