---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "principal",
      "effect": "creates"
    }
  ],
  "permits": [
    {
      "configuredBy": "project-invitation"
    },
    {
      "configuredBy": "public-join-policy"
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
      "target": "apps/worker/src/services/invitations.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/public-join.ts"
    }
  ]
}
---

# Only a matched unauthenticated ordinary offer or public join creates its new Principal (create Principal)

Match this request's submitted code digest to the exact ordinary Project invitation. Require its current unrevoked, unredeemed, unexpired offer and the recorded issuing administrator ID/generation still active; all offered targets must exist and their Project and Workspace parents must be active. New-principal mode requires an unauthenticated request and creates its explicit new Principal and Credential. Current-principal mode requires current authentication, refuses Owner, and creates no Credential. Cookie is accepted only for current-principal ordinary invitations: project_selection has its own allowed branch; otherwise every offered target must both be currently accessible and fall inside the fixed Workspace/Project/Issue Session scope. Any out-of-scope target rejects the entire multi-target redemption. Capacity, display-name and replacement-token conflicts are checked before the atomic grant/redemption/audit commit. Applicable same-operation replay verifies its bound inputs and current Cookie scope rather than redeeming a second time.

Bind the submitted public ID to its actual Project Public join policy, rather than an invitation token. A new commit requires an enabled policy, active Project and Workspace, usage row and finite configured Issue, Comment and Principal limits; reader and writer are the established role choices. New-principal mode must be unauthenticated and supplies a new name and replacement token. Current-principal mode requires current authentication and rejects Owner. A project_selection Cookie may join this target; other Cookie targets must already resolve it inside live allowed scope and admin Cookie is refused. Check Principal capacity for a newly effective member, without charging an already effective source twice. Direct reader may become writer, writer is never downgraded, and a revoked direct grant may be regranted. Applicable replay may use the requester's existing active public-join grant even when the policy has subsequently been disabled, after current identity and Cookie-scope checks; unauthenticated token replay authenticates that exact replacement Credential and requires its active public-join grant. This replay does not authorize a new write under a disabled policy.

Only each configuration's new-principal branch creates a Principal; current-principal acceptance and recovery reuse their existing identity. No requester Principal is invented before creation.
