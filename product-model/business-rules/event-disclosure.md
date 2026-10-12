---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "event",
      "effect": "reads"
    }
  ],
  "permits": [
    {
      "configuredBy": "principal"
    },
    {
      "configuredBy": "instance"
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
      "target": "apps/worker/src/services/events.ts"
    }
  ]
}
---

# Only current domain visibility or Owner control reads the selected Event stream (read Event)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

The Principal branch selects domain history inside this request's current visible Projects/Workspace scope and active-parent rules; a Relation Event also requires current visibility of relation_other_project_id, so one visible endpoint is insufficient. Retain cursor/principal/scope binding and current guard before returning. Security and all-stream audit retrieval are admitted only by the Instance Owner-control branch, including its exact bearer/admin-Cookie restriction; domain visibility never authorizes audit metadata.

The Instance configuration selects its retained Owner principal ID. The authenticated request Principal must equal that ID. Owner control accepts bearer, or a Cookie Session whose target kind is admin; a fixed Workspace, Project, Issue or project_selection Cookie is not Owner control. Scoped administrator grants cannot satisfy this branch. Recheck the retained Owner binding and current authentication for the guarded operation.
