---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "passkey",
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
      "target": "apps/worker/src/services/passkeys.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/auth.ts"
    }
  ]
}
---

# Only a current Credential-sourced Cookie Principal registers its own Passkey (create Passkey)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

Registration requires the current Cookie Session with Credential source, linked to the same Principal and source Credential as the retained registration challenge; bearer and Passkey-sourced Cookie are refused for registration. Preserve same ceremony origin/RP, challenge expiry/one-use and active authenticator limit. These ceremony validations establish authentication, not invented stored authorization flags.
