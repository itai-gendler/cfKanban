---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "notification-acknowledgement",
      "effect": "creates"
    }
  ],
  "permits": [
    {
      "configuredBy": "principal"
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
      "target": "apps/worker/src/kernel/auth.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/authorization.ts"
    }
  ]
}
---

# Only an authenticated non-publisher recipient records its own acknowledgement (create Notification acknowledgement)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

Bind the acknowledgement to the current Principal and selected existing notification. Reject missing notification or a notification published by that same Principal. First acknowledgement is retained; repeat acknowledgement preserves that one record and its initial timestamp. A repeat with a new idempotency key can record another security event; replay of the same committed request does not rerun the commit. No other Principal's acknowledgement is editable.
