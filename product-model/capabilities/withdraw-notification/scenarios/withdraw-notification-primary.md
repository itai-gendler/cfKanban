---
{
  "kind": "primary",
  "routes": {
    "wa": "Wa entry",
    "ro": "Ro entry",
    "co": "Co entry"
  },
  "steps": [
    {
      "text": "Request withdrawal of the selected published notice at its current version.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::notifications"
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
      "text": "撤回公告",
      "kind": "product",
      "entities": [
        {
          "entity": "notification",
          "effect": "changes",
          "facts": [
            "Withdrawn at",
            "Version"
          ],
          "from": "Active",
          "to": "Withdrawn"
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::notifications"
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
      "target": "apps/worker/src/services/notifications.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Withdraw notification primary

## Trigger

Request withdrawal of the selected published notice at its current version.

## Outcome

撤回公告

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Reading does not acknowledge. Publisher cannot acknowledge their own notice. Expired and withdrawn history remain. Expiry is calculated; reenable resets receive-after. Published title/body cannot be edited.
- This operation retains the idempotent-cas contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- An already withdrawn publication is refused. An expired but unwithdrawn publication can still be withdrawn at its current version.
