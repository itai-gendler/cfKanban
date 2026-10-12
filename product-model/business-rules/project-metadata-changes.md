---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "project",
      "effect": "changes",
      "facts": [
        "Name",
        "Context",
        "Version",
        "Updated at"
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/public-join.ts"
    }
  ]
}
---

# The current operation’s configured source governs Project metadata and atomic concurrency updates

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

Resolve the management source for the operation and exact Workspace/Project IDs selected by this request. Bearer has no Cookie target restriction. Cookie admin admits only Owner; project_selection admits only a non-Owner; Workspace target must match the selected Workspace; fixed Project/Issue management must match both Workspace and Project, have a Project scope, and is refused to Owner. Workspace management cannot be obtained from a fixed Project/Issue Session. For an allowed non-Owner source, select the live administrator grant by Principal, scope, unrevoked state and current ID/generation; retain and recheck that ID/generation in the commit guard. Owner is identified only by Instance Owner principal equality. Workspace grants take precedence when both administrator sources apply. Non-Owner requires an active Workspace; Project administrator requires an active Project. Regrant changes generation and does not revive invitations issued against an old generation.


Name/context and status-name writes resolve manage_project on active parents: retained Owner, matching Workspace administrator or matching Project administrator. Archive/restore bookkeeping uses the implemented archive_project guard, restricted to retained Owner or matching Workspace administrator with its actual archived-Project exception; it does not confer ordinary data access. Public-join enable/disable and resource-limit writes require the exact retained Instance Owner under Owner control (bearer or admin Cookie), not a fixed-target Cookie or a scoped administrator source.

Version and updated time advance only within the containing atomic operation. Resolve the above configuration from that actual operation and target; these facts introduce no independent permission, and their selector cannot substitute a more permissive management branch for the endpoint’s guard.
