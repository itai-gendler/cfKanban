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
      "text": "Submit a positive finite byte limit or unlimited capacity at the current version.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wo": {
          "place": "online-web::administration::attachment-capacity"
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
      "text": "保存有限/无限容量设置",
      "kind": "product",
      "entities": [
        {
          "entity": "attachment-capacity",
          "effect": "changes",
          "facts": [
            "Configured",
            "Limit",
            "Version"
          ],
          "from": "Unconfigured",
          "to": "Configured"
        }
      ],
      "contexts": {
        "wo": {
          "place": "online-web::administration::attachment-capacity"
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
      "target": "apps/worker/src/services/attachment-settings.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Change attachment storage settings primary

## Trigger

Submit a positive finite byte limit or unlimited capacity; the successful operation records that the limit is configured.

## Outcome

保存有限/无限容量设置

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Storage availability differs from metadata availability. Size is one byte through 10 MiB, actual digest/size must match, at most twenty active/pending slots and reserved-byte capacity apply. Pending cancellation is not Ready restoration. Soft deletion does not immediately release budget.
- This operation retains the idempotent-cas contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
