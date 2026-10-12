---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "workspace",
      "effect": "reads",
      "facts": [
        "Trend history",
        "Trend coverage"
      ]
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
      "target": "apps/worker/src/services/issue-trends.ts"
    }
  ]
}
---

# Only current Workspace management sources read enabled Workspace trends (read Workspace Trend history, Trend coverage)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

Resolve the management source for the operation and exact Workspace/Project IDs selected by this request. Bearer has no Cookie target restriction. Cookie admin admits only Owner; project_selection admits only a non-Owner; Workspace target must match the selected Workspace; fixed Project/Issue management must match both Workspace and Project, have a Project scope, and is refused to Owner. Workspace management cannot be obtained from a fixed Project/Issue Session. For an allowed non-Owner source, select the live administrator grant by Principal, scope, unrevoked state and current ID/generation; retain and recheck that ID/generation in the commit guard. Owner is identified only by Instance Owner principal equality. Workspace grants take precedence when both administrator sources apply. Non-Owner requires an active Workspace; Project administrator requires an active Project. Regrant changes generation and does not revive invitations issued against an old generation.

Resolve manage_workspace for the selected Workspace: retained Owner or matching Workspace administrator, not Project administrator. Require enabled trends and refuse Issue-bound/fixed Project Sessions that cannot manage Workspace. Aggregate all active Projects within this scope and refuse more than one hundred; history and range bounds remain.
