---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "browser-launch",
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
    }
  ]
}
---

# Only an authenticated bearer with exact target authority creates Browser launch (create Browser launch)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

Require bearer and bind launch Principal/source Credential to that exact request. Resolve Workspace through manage_workspace; Project through its current Project access; Issue through its current active Issue and Project access; admin through retained Instance Owner equality and bearer-only Owner control. Refuse targets outside current authority and persist only the resolved target and entry. Recheck source and target in the creation guard.
