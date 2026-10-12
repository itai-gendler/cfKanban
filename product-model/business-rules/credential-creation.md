---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "credential",
      "effect": "creates"
    }
  ],
  "permits": [
    {
      "configuredBy": "project-invitation"
    },
    {
      "configuredBy": "recovery-invitation"
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/auth.ts"
    }
  ]
}
---

# Only a matched new-identity or recovery offer creates its exact Credential (create Credential)

Match this request's submitted code digest to the exact ordinary Project invitation. Require its current unrevoked, unredeemed, unexpired offer and the recorded issuing administrator ID/generation still active; all offered targets must exist and their Project and Workspace parents must be active. New-principal mode requires an unauthenticated request and creates its explicit new Principal and Credential. Current-principal mode requires current authentication, refuses Owner, and creates no Credential. Cookie is accepted only for current-principal ordinary invitations: project_selection has its own allowed branch; otherwise every offered target must both be currently accessible and fall inside the fixed Workspace/Project/Issue Session scope. Any out-of-scope target rejects the entire multi-target redemption. Capacity, display-name and replacement-token conflicts are checked before the atomic grant/redemption/audit commit. Applicable same-operation replay verifies its bound inputs and current Cookie scope rather than redeeming a second time.

Match the submitted code digest to the exact valid, unrevoked, unredeemed, unexpired recovery invitation and its bound non-Owner Principal. Full recovery permits a holder without authentication; if authentication is supplied its Principal must match the bound Principal. Rotation requires a current matching bearer Credential; Cookie is refused for either recovery mode. Create only the replacement Credential for the bound Principal. Full recovery revokes every previously active Credential for that Principal; rotation revokes only the Credential authenticating this request. Neither mode creates a new Principal, changes its Project grants or assignments, nor revokes Passkeys. Preserve atomic consumption, replacement, revocations and security audit and the matching-input replay boundary.

Bind the submitted public ID to its actual Project Public join policy, rather than an invitation token. A new commit requires an enabled policy, active Project and Workspace, usage row and finite configured Issue, Comment and Principal limits; reader and writer are the established role choices. New-principal mode must be unauthenticated and supplies a new name and replacement token. Current-principal mode requires current authentication and rejects Owner. A project_selection Cookie may join this target; other Cookie targets must already resolve it inside live allowed scope and admin Cookie is refused. Check Principal capacity for a newly effective member, without charging an already effective source twice. Direct reader may become writer, writer is never downgraded, and a revoked direct grant may be regranted. Applicable replay may use the requester's existing active public-join grant even when the policy has subsequently been disabled, after current identity and Cookie-scope checks; unauthenticated token replay authenticates that exact replacement Credential and requires its active public-join grant. This replay does not authorize a new write under a disabled policy.

These OR configurations each authorize only their own implemented branch: new ordinary/public identity creation, or a replacement for the recovery-bound Principal. Current ordinary invitation/public join creates no Credential. Never accept one branch's configuration as a bypass for another. Retain replacement-token uniqueness and private trusted delivery.
