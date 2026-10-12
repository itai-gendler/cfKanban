---
{
  "kind": "primary",
  "routes": {
    "wa": "Wa entry",
    "ra": "Ra entry",
    "ca": "Ca entry"
  },
  "steps": [
    {
      "text": "Select an enabled public offer and allowed role.",
      "kind": "actor",
      "actor": "participant",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::authenticated-home"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      }
    },
    {
      "text": "重新建立已撤销 direct grant",
      "kind": "product",
      "entities": [
        {
          "entity": "project-grant",
          "effect": "changes",
          "facts": [
            "Role",
            "Version",
            "Revoked at",
            "Revoked by"
          ],
          "from": "Revoked",
          "to": "Active"
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::authenticated-home"
        },
        "ra": {
          "place": "rest-api::authenticated"
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

# Join public project regrant

## Trigger

Select an enabled public offer and allowed role.

## Outcome

重新建立已撤销 direct grant

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Public summaries provide no anonymous Board access. Enabled roles and effective capacity are checked atomically. Existing Writer is not downgraded and revoked direct access may be regranted.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- A mixed current/new mode is refused; the new mode cannot carry authentication. A current Owner, invalid identity source or fixed Cookie target outside live scope is refused. project_selection retains its separate acceptance branch. A disabled policy rejects a new commit; matching replay through an existing active public-join grant retains the original result. New effective membership at capacity fails atomically.
