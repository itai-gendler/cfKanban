---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "passkey",
      "effect": "changes",
      "facts": [
        "Revoked at"
      ]
    }
  ],
  "permits": [
    {
      "configuredBy": "principal"
    },
    {
      "configuredBy": "instance"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/passkeys.ts"
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

# Only the current own Principal or Owner control revokes a selected allowed Passkey (change Passkey Revoked at)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

The self endpoint accepts bearer or Cookie and requires that exact authenticator belongs to the current Principal. Owner control management targets only a non-Owner Principal's selected active Passkey; it cannot revoke Owner through the ordinary management branch. Preserve current version and revocation state and source-linked Session invalidation.

The Instance configuration selects its retained Owner principal ID. The authenticated request Principal must equal that ID. Owner control accepts bearer, or a Cookie Session whose target kind is admin; a fixed Workspace, Project, Issue or project_selection Cookie is not Owner control. Scoped administrator grants cannot satisfy this branch. Recheck the retained Owner binding and current authentication for the guarded operation.
