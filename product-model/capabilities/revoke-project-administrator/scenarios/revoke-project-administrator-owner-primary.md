---
{
  "kind": "primary",
  "routes": {
    "wo": "Wo entry",
    "ro": "Ro entry",
    "co": "Co entry"
  },
  "steps": [
    {
      "text": "Request revoking the selected scoped management source with its current version.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wo": {
          "place": "online-web::administration::access"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        }
      }
    },
    {
      "text": "实例所有者/WAdmin 撤销 项目 admin grant",
      "kind": "product",
      "entities": [
        {
          "entity": "project-administrator-grant",
          "effect": "changes",
          "facts": [
            "Revoked at",
            "Revoked by",
            "Version"
          ],
          "from": "Active",
          "to": "Revoked"
        }
      ],
      "contexts": {
        "wo": {
          "place": "online-web::administration::access"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        }
      },
      "actor": "owner"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/scoped-administrators.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Revoke project administrator owner primary

## Trigger

Request revoking the selected scoped management source with its current version.

## Outcome

Owner/WAdmin 撤销 Project admin grant

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- This operation retains the idempotent-cas-delete contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
