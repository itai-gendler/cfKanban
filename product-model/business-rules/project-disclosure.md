---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "project",
      "effect": "reads",
      "facts": [
        "Identity",
        "Context",
        "Created at",
        "Updated at",
        "Version",
        "Archived at",
        "Archived by"
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
      "target": "apps/worker/src/services/containers.ts"
    }
  ]
}
---

# Only current Project data or operation-specific management sources read metadata (read Project Identity, Context, Created at and other selected metadata)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

Resolve the exact target Project through the selected object, its Issue or the selected relation endpoint. The request Principal must have an effective source in that Project: an unrevoked direct reader/writer grant, an unrevoked Workspace administrator grant inherited by its Projects, an unrevoked Project administrator grant for that Project, or equality with the retained Instance Owner principal. Merge independent sources with writer taking precedence; removing one source does not remove another. Ordinary reads and writes require active Project and Workspace parents. Cookie scope is intersected with live visibility: Workspace target matches its Workspace, fixed Project matches both IDs, and fixed Issue resolves its still-active Issue and Project; it cannot broaden the allowed Projects. Bearer does not inherit Cookie target limits. Owner data access is distinct from Owner control and does not make a fixed Session an administration Session.

Ordinary Project list/detail resolves current visible Projects; management responses use the exact management operation. Deleted-only list/detail requires Owner control or matching Workspace create_project/archive management, never ordinary Reader or Project administrator. The archive exception is confined to that endpoint and retains Workspace checks.

Resolve the management source for the operation and exact Workspace/Project IDs selected by this request. Bearer has no Cookie target restriction. Cookie admin admits only Owner; project_selection admits only a non-Owner; Workspace target must match the selected Workspace; fixed Project/Issue management must match both Workspace and Project, have a Project scope, and is refused to Owner. Workspace management cannot be obtained from a fixed Project/Issue Session. For an allowed non-Owner source, select the live administrator grant by Principal, scope, unrevoked state and current ID/generation; retain and recheck that ID/generation in the commit guard. Owner is identified only by Instance Owner principal equality. Workspace grants take precedence when both administrator sources apply. Non-Owner requires an active Workspace; Project administrator requires an active Project. Regrant changes generation and does not revive invitations issued against an old generation.
