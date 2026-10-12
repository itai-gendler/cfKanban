---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "web-session",
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
      "target": "apps/worker/src/kernel/scoped-authorization.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/web-auth.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/web-session-state.ts"
    }
  ]
}
---

# Only the exact current Cookie Session source reads its own scope projection (read Web session)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

Bind target identity to the current Cookie sessionId as well as Principal. Return only this Session/source/target and live allowed scope, not other Sessions of that Principal. Recheck current visible Projects with authentication in the same guard; Workspace target requires current manage_workspace, admin requires Owner, fixed Project/Issue requires still-visible matching active scope, and project_selection retains its selector behavior. No bearer Session-inventory branch exists.
