---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "project-grant",
      "effect": "changes"
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
      "target": "apps/worker/src/kernel/scoped-authorization.ts"
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/public-join.ts"
    }
  ]
}
---

# Only exact member-management or matched offer sources write Project grants (change Project grant)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

The Principal configuration branch resolves manage_members for the selected Project, allowing retained Owner, matching Workspace administrator or matching Project administrator under the precise management scope. Target Principal must not be Owner. Direct reader/writer changes, revocation and regrant preserve independent administrator sources and assignments; applicable member quotas remain.

Resolve the management source for the operation and exact Workspace/Project IDs selected by this request. Bearer has no Cookie target restriction. Cookie admin admits only Owner; project_selection admits only a non-Owner; Workspace target must match the selected Workspace; fixed Project/Issue management must match both Workspace and Project, have a Project scope, and is refused to Owner. Workspace management cannot be obtained from a fixed Project/Issue Session. For an allowed non-Owner source, select the live administrator grant by Principal, scope, unrevoked state and current ID/generation; retain and recheck that ID/generation in the commit guard. Owner is identified only by Instance Owner principal equality. Workspace grants take precedence when both administrator sources apply. Non-Owner requires an active Workspace; Project administrator requires an active Project. Regrant changes generation and does not revive invitations issued against an old generation.

The ordinary invitation configuration branch grants only its offered targets/roles to its new or current redeemer; it does not authorize unrelated grant administration.

Match this request's submitted code digest to the exact ordinary Project invitation. Require its current unrevoked, unredeemed, unexpired offer and the recorded issuing administrator ID/generation still active; all offered targets must exist and their Project and Workspace parents must be active. New-principal mode requires an unauthenticated request and creates its explicit new Principal and Credential. Current-principal mode requires current authentication, refuses Owner, and creates no Credential. Cookie is accepted only for current-principal ordinary invitations: project_selection has its own allowed branch; otherwise every offered target must both be currently accessible and fall inside the fixed Workspace/Project/Issue Session scope. Any out-of-scope target rejects the entire multi-target redemption. Capacity, display-name and replacement-token conflicts are checked before the atomic grant/redemption/audit commit. Applicable same-operation replay verifies its bound inputs and current Cookie scope rather than redeeming a second time.

The Public join policy branch grants only the actual joined target/role and its promotion/regrant/no-downgrade semantics.

Bind the submitted public ID to its actual Project Public join policy, rather than an invitation token. A new commit requires an enabled policy, active Project and Workspace, usage row and finite configured Issue, Comment and Principal limits; reader and writer are the established role choices. New-principal mode must be unauthenticated and supplies a new name and replacement token. Current-principal mode requires current authentication and rejects Owner. A project_selection Cookie may join this target; other Cookie targets must already resolve it inside live allowed scope and admin Cookie is refused. Check Principal capacity for a newly effective member, without charging an already effective source twice. Direct reader may become writer, writer is never downgraded, and a revoked direct grant may be regranted. Applicable replay may use the requester's existing active public-join grant even when the policy has subsequently been disabled, after current identity and Cookie-scope checks; unauthenticated token replay authenticates that exact replacement Credential and requires its active public-join grant. This replay does not authorize a new write under a disabled policy.
