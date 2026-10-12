---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "project-invitation",
      "effect": "changes",
      "facts": [
        "Redeemed at",
        "Redeemed by"
      ]
    }
  ],
  "permits": [
    {
      "configuredBy": "project-invitation"
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
      "target": "apps/worker/src/kernel/scoped-authorization.ts"
    }
  ]
}
---

# Only the matched valid ordinary invitation authorizes its exact redemption (change Project invitation Redeemed at, Redeemed by)

Match this request's submitted code digest to the exact ordinary Project invitation. Require its current unrevoked, unredeemed, unexpired offer and the recorded issuing administrator ID/generation still active; all offered targets must exist and their Project and Workspace parents must be active. New-principal mode requires an unauthenticated request and creates its explicit new Principal and Credential. Current-principal mode requires current authentication, refuses Owner, and creates no Credential. Cookie is accepted only for current-principal ordinary invitations: project_selection has its own allowed branch; otherwise every offered target must both be currently accessible and fall inside the fixed Workspace/Project/Issue Session scope. Any out-of-scope target rejects the entire multi-target redemption. Capacity, display-name and replacement-token conflicts are checked before the atomic grant/redemption/audit commit. Applicable same-operation replay verifies its bound inputs and current Cookie scope rather than redeeming a second time.
