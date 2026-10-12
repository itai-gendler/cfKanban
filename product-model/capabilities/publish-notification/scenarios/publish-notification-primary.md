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
      "text": "Submit title, immutable body and expiry.",
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
      "text": "发布不可编辑公告",
      "kind": "product",
      "entities": [
        {
          "entity": "notification",
          "effect": "creates",
          "facts": [
            "Identity",
            "Title",
            "Body",
            "Publisher",
            "Published at",
            "Expires at",
            "Withdrawn at",
            "Version",
            "Visible status"
          ],
          "to": "Active"
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

# Publish notification primary

## Trigger

Submit title, immutable body and expiry.

## Outcome

发布不可编辑公告

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Reading does not acknowledge. Publisher cannot acknowledge their own notice. Expired and withdrawn history remain. Expiry is calculated; reenable resets receive-after. Published title/body cannot be edited.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
