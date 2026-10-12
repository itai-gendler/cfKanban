---
{
  "kind": "primary",
  "routes": {
    "wa": "Wa entry",
    "ca": "Ca entry"
  },
  "steps": [
    {
      "text": "Request public identity, summary, allowed roles for the explicit collection, filters and bounded cursor.",
      "kind": "actor",
      "actor": "participant",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::authenticated-home"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      }
    },
    {
      "text": "读取同一公开摘要",
      "kind": "product",
      "entities": [
        {
          "entity": "public-join-policy",
          "effect": "reads",
          "facts": [
            "Public identity",
            "Summary",
            "Allowed roles"
          ]
        },
        {
          "entity": "project",
          "effect": "reads",
          "facts": [
            "Name"
          ]
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::authenticated-home"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      },
      "actor": "participant"
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
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Browse public projects authenticated

## Trigger

Request public identity, summary, allowed roles for the explicit collection, filters and bounded cursor.

## Outcome

读取同一公开摘要

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
- Public summaries provide no anonymous Board access. Enabled roles and effective capacity are checked atomically. Existing Writer is not downgraded and revoked direct access may be regranted.
