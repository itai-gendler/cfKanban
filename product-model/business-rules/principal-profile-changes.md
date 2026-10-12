---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "principal",
      "effect": "changes",
      "facts": [
        "Display name",
        "Preferred language",
        "Appearance",
        "Profile version",
        "Updated at"
      ]
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
      "target": "apps/worker/src/kernel/authorization.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/auth.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/identity.ts"
    }
  ]
}
---

# Only the current request Principal changes its own profile (change Principal Display name, Preferred language, Appearance and other selected metadata)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

Select only the record or preference owned by the authenticated request Principal. This is a request-to-record match through the retained Principal linkage, not self: true and not access to every record associated with another Principal.

Update display name, locale or theme only on that Principal with its current profile version and actual endpoint write contract; Owner does not gain an edit-another-profile branch.
