---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "workspace",
      "effect": "reads",
      "facts": [
        "Name"
      ]
    }
  ],
  "permits": [
    {
      "configuredBy": "principal"
    },
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
      "target": "apps/worker/src/kernel/auth.ts"
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
      "target": "apps/worker/src/services/public-join-sql.ts"
    }
  ]
}
---

# Only current access or matched invitation and join-result sources disclose a Workspace name (read Workspace Name)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

The Principal branch discloses names in the current visible-scope or exact management projection, with its actual Grant/Session scope. The invitation branch returns the names of its matched valid offered targets for holder preview or the authorized redemption result; it uses the exact HOLDER/OFFER policies below. The public-join branch discloses the target Workspace name only in a successful authorized join result, not the anonymous public Project discovery list. An enabled public policy alone grants no anonymous Workspace-name discovery.

Match the submitted code digest to this exact invitation. Non-consuming preview requires an unrevoked, unredeemed, unexpired invitation and a currently valid issuing administrator ID/generation when one was retained. Reject unknown code, revoked, redeemed, expired or invalidated issuer with the implemented validation/not-found/gone response; no invalid invitation detail is disclosed as a successful preview. A holder need not have a request Principal. Management retrieval is a separate authenticated branch and does not require possession of the code.

Match this request's submitted code digest to the exact ordinary Project invitation. Require its current unrevoked, unredeemed, unexpired offer and the recorded issuing administrator ID/generation still active; all offered targets must exist and their Project and Workspace parents must be active. New-principal mode requires an unauthenticated request and creates its explicit new Principal and Credential. Current-principal mode requires current authentication, refuses Owner, and creates no Credential. Cookie is accepted only for current-principal ordinary invitations: project_selection has its own allowed branch; otherwise every offered target must both be currently accessible and fall inside the fixed Workspace/Project/Issue Session scope. Any out-of-scope target rejects the entire multi-target redemption. Capacity, display-name and replacement-token conflicts are checked before the atomic grant/redemption/audit commit. Applicable same-operation replay verifies its bound inputs and current Cookie scope rather than redeeming a second time.

Bind the submitted public ID to its actual Project Public join policy, rather than an invitation token. A new commit requires an enabled policy, active Project and Workspace, usage row and finite configured Issue, Comment and Principal limits; reader and writer are the established role choices. New-principal mode must be unauthenticated and supplies a new name and replacement token. Current-principal mode requires current authentication and rejects Owner. A project_selection Cookie may join this target; other Cookie targets must already resolve it inside live allowed scope and admin Cookie is refused. Check Principal capacity for a newly effective member, without charging an already effective source twice. Direct reader may become writer, writer is never downgraded, and a revoked direct grant may be regranted. Applicable replay may use the requester's existing active public-join grant even when the policy has subsequently been disabled, after current identity and Cookie-scope checks; unauthenticated token replay authenticates that exact replacement Credential and requires its active public-join grant. This replay does not authorize a new write under a disabled policy.
