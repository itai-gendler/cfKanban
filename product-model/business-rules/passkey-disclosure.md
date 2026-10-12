---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "passkey",
      "effect": "reads",
      "facts": [
        "Identity",
        "Principal",
        "Authenticator description",
        "Created at",
        "Last used at",
        "Version",
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/access.ts"
    }
  ]
}
---

# Only own authenticator inventory or Owner metadata reads selected Passkey facts (read Passkey Identity, Principal, Authenticator description and other selected metadata)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

The own branch accepts current bearer or Cookie and restricts inventory to that Principal's nonsecret authenticators; authentication/sign-in verification reads the authenticator matched by the assertion, not a public inventory. Owner control may read the actual nonsecret management summary for a selected Principal.

The Instance configuration selects its retained Owner principal ID. The authenticated request Principal must equal that ID. Owner control accepts bearer, or a Cookie Session whose target kind is admin; a fixed Workspace, Project, Issue or project_selection Cookie is not Owner control. Scoped administrator grants cannot satisfy this branch. Recheck the retained Owner binding and current authentication for the guarded operation.
