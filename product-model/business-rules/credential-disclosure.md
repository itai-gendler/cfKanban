---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "credential",
      "effect": "reads"
    }
  ],
  "permits": [
    {
      "configuredBy": "instance"
    },
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
      "target": "apps/worker/src/services/access.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/identity.ts"
    }
  ]
}
---

# Only Owner control or the exact own-source projection reads nonsecret Credential metadata (read Credential)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

The Instance configuration selects its retained Owner principal ID. The authenticated request Principal must equal that ID. Owner control accepts bearer, or a Cookie Session whose target kind is admin; a fixed Workspace, Project, Issue or project_selection Cookie is not Owner control. Scoped administrator grants cannot satisfy this branch. Recheck the retained Owner binding and current authentication for the guarded operation.

The Principal branch returns only the current bearer Credential's necessary ID/fingerprint in /me or identity inspection, or exact replacement delivery metadata in the corresponding successful operation. It is not a grant to browse all of that Principal's Credentials. Owner inventory remains nonsecret management metadata; bearer tokens are never a displayed fact.
