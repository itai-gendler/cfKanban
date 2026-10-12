---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "project-invitation",
      "effect": "reads",
      "facts": [
        "Project targets",
        "Roles",
        "Expires at"
      ]
    }
  ],
  "permits": [
    {
      "configuredBy": "project-invitation"
    },
    {
      "configuredBy": "principal"
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/scoped-authorization.ts"
    }
  ]
}
---

# Only the matched valid holder or exact all-target manager reads offered preview facts (read Project invitation Project targets, Roles, Expires at)

Match the submitted code digest to this exact invitation. Non-consuming preview requires an unrevoked, unredeemed, unexpired invitation and a currently valid issuing administrator ID/generation when one was retained. Reject unknown code, revoked, redeemed, expired or invalidated issuer with the implemented validation/not-found/gone response; no invalid invitation detail is disclosed as a successful preview. A holder need not have a request Principal. Management retrieval is a separate authenticated branch and does not require possession of the code.

The Principal branch is only authenticated management retrieval, requiring Owner control or manage_members for every offered target with the precise Session scope and current source/generation. It may return retained management history; it is not the unauthenticated holder-preview branch.

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

The Instance configuration selects its retained Owner principal ID. The authenticated request Principal must equal that ID. Owner control accepts bearer, or a Cookie Session whose target kind is admin; a fixed Workspace, Project, Issue or project_selection Cookie is not Owner control. Scoped administrator grants cannot satisfy this branch. Recheck the retained Owner binding and current authentication for the guarded operation.

Resolve the management source for the operation and exact Workspace/Project IDs selected by this request. Bearer has no Cookie target restriction. Cookie admin admits only Owner; project_selection admits only a non-Owner; Workspace target must match the selected Workspace; fixed Project/Issue management must match both Workspace and Project, have a Project scope, and is refused to Owner. Workspace management cannot be obtained from a fixed Project/Issue Session. For an allowed non-Owner source, select the live administrator grant by Principal, scope, unrevoked state and current ID/generation; retain and recheck that ID/generation in the commit guard. Owner is identified only by Instance Owner principal equality. Workspace grants take precedence when both administrator sources apply. Non-Owner requires an active Workspace; Project administrator requires an active Project. Regrant changes generation and does not revive invitations issued against an old generation.

The selected read is limited to the endpoint's returned projection. Issuer/source generation and code digest are retained validation/audit configuration, not successful holder-preview or management-inventory fields. A management read does not disclose plaintext codes or internal digest values.
