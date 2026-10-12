---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "notification-preferences",
      "effect": "reads"
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

# Only the current Principal reads or changes its own notification preferences (read Notification preferences)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

Select only the record or preference owned by the authenticated request Principal. This is a request-to-record match through the retained Principal linkage, not self: true and not access to every record associated with another Principal.

A reception update compares the current preference version and advances it on commit. Re-enabling after disabled reception resets receive-after to that update time; other updates preserve the existing lower boundary, no earlier than identity creation. Owner does not gain another Principal's preferences. Disabled reception yields no pending items without hiding permitted historical personal notifications.
