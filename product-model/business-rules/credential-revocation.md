---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "credential",
      "effect": "changes",
      "facts": [
        "Revoked at"
      ]
    }
  ],
  "permits": [
    {
      "configuredBy": "instance"
    },
    {
      "configuredBy": "recovery-invitation"
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
      "target": "apps/worker/src/services/access.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/invitations.ts"
    }
  ]
}
---

# Only Owner control or the exact recovery offer revokes its selected Credentials (change Credential Revoked at)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

The Instance configuration selects its retained Owner principal ID. The authenticated request Principal must equal that ID. Owner control accepts bearer, or a Cookie Session whose target kind is admin; a fixed Workspace, Project, Issue or project_selection Cookie is not Owner control. Scoped administrator grants cannot satisfy this branch. Recheck the retained Owner binding and current authentication for the guarded operation.

Owner management revocation targets an existing non-Owner Principal's selected Credential; it cannot revoke Owner through this ordinary path. The recovery configuration is an alternative only inside the exact recovery transaction, with the following full/rotation revocation scope.

Match the submitted code digest to the exact valid, unrevoked, unredeemed, unexpired recovery invitation and its bound non-Owner Principal. Full recovery permits a holder without authentication; if authentication is supplied its Principal must match the bound Principal. Rotation requires a current matching bearer Credential; Cookie is refused for either recovery mode. Create only the replacement Credential for the bound Principal. Full recovery revokes every previously active Credential for that Principal; rotation revokes only the Credential authenticating this request. Neither mode creates a new Principal, changes its Project grants or assignments, nor revokes Passkeys. Preserve atomic consumption, replacement, revocations and security audit and the matching-input replay boundary.
