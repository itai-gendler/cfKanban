---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "public-join-policy",
      "effect": "reads",
      "facts": [
        "Public identity",
        "Summary",
        "Allowed roles"
      ]
    }
  ],
  "permits": [
    {
      "configuredBy": "public-join-policy"
    },
    {
      "configuredBy": "instance"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/public-join.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/public-join-sql.ts"
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
    }
  ]
}
---

# Only an exact enabled public policy or Owner control discloses public offer facts (read Public join policy Public identity, Summary, Allowed roles)

The public policy configuration matches the selected discovery row: enabled_at present, disabled_at absent, active Project and Workspace, usage row and finite configured Issue/Comment/Principal limits. Disclose only Project display name, public ID, public summary and reader/writer choices. No Workspace name, private Board data, limits or usage is disclosed by anonymous discovery. The Instance branch returns these fields only as part of Owner-controlled policy management.

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

The Instance configuration selects its retained Owner principal ID. The authenticated request Principal must equal that ID. Owner control accepts bearer, or a Cookie Session whose target kind is admin; a fixed Workspace, Project, Issue or project_selection Cookie is not Owner control. Scoped administrator grants cannot satisfy this branch. Recheck the retained Owner binding and current authentication for the guarded operation.
