---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "recovery-invitation",
      "effect": "changes",
      "facts": [
        "Redeemed at",
        "Redeemed by"
      ]
    }
  ],
  "permits": [
    {
      "configuredBy": "recovery-invitation"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/invitations.ts"
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

# Only the matched recovery offer with its mode-bound source authorizes consumption (change Recovery invitation Redeemed at, Redeemed by)

Match the submitted code digest to the exact valid, unrevoked, unredeemed, unexpired recovery invitation and its bound non-Owner Principal. Full recovery permits a holder without authentication; if authentication is supplied its Principal must match the bound Principal. Rotation requires a current matching bearer Credential; Cookie is refused for either recovery mode. Create only the replacement Credential for the bound Principal. Full recovery revokes every previously active Credential for that Principal; rotation revokes only the Credential authenticating this request. Neither mode creates a new Principal, changes its Project grants or assignments, nor revokes Passkeys. Preserve atomic consumption, replacement, revocations and security audit and the matching-input replay boundary.
