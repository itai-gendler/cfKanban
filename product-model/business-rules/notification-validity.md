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
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/notifications.ts"
    }
  ]
}
---

# 正文不可改；到期计算；打开不确认

Published title and body are immutable. Expiry is calculated from time without an expiry write or audit event. Opening the page or badge never acknowledges; explicit acknowledgement records its first timestamp. Withdrawal is a separate versioned write and remains possible for expired, unwithdrawn notices.
