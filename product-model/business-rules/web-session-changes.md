---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "web-session",
      "effect": "changes"
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
      "target": "apps/worker/src/services/web-auth.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/web-session-renewal.ts"
    }
  ]
}
---

# Only the exact current Cookie Session or its validated source invalidation changes Session state (change Web session)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

Renewal and logout select current Cookie sessionId and Principal, not all Sessions of that Principal. Renewal preserves the exact authentication source and target, rechecks its live scope (admin Owner; Workspace management; active fixed Project/Issue authorization; project_selection), and retains its version, renewal interval and absolute cap. Not-due renewal is a no-op. Logout revokes only this current Session. Retained source-Credential/Passkey revocation may invalidate its linked Sessions only inside that authorized source revocation; it grants no independent bulk-Session edit. Expiry is computed from time, not a caller's authorized write.
