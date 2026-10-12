---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "issue",
      "effect": "changes",
      "facts": [
        "Title",
        "Body",
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
      "target": "migrations/0009_scoped_administrators.sql"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/issues.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/relations.ts"
    }
  ]
}
---

# Current Project writer sources govern Issue content and atomic concurrency updates

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

Resolve the exact target Project through the selected object, its Issue or the selected relation endpoint. The request Principal must have an effective source in that Project: an unrevoked direct reader/writer grant, an unrevoked Workspace administrator grant inherited by its Projects, an unrevoked Project administrator grant for that Project, or equality with the retained Instance Owner principal. Merge independent sources with writer taking precedence; removing one source does not remove another. Ordinary reads and writes require active Project and Workspace parents. Cookie scope is intersected with live visibility: Workspace target matches its Workspace, fixed Project matches both IDs, and fixed Issue resolves its still-active Issue and Project; it cannot broaden the allowed Projects. Bearer does not inherit Cookie target limits. Owner data access is distinct from Owner control and does not make a fixed Session an administration Session.

Require writer or stronger for this selected write.

The selected Issue version and updated time are bookkeeping of its actual containing write, not a separately configurable right. For a relation operation, resolve this configuration for each aliased endpoint Issue; both endpoint Rules and versions must also pass. Completion retains its separate Done-entry and evidence guards. No field-level grant bypasses these operation guards.
