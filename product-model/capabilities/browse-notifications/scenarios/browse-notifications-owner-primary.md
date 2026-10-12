---
{
  "kind": "primary",
  "routes": {
    "ro": "Ro entry",
    "co": "Co entry"
  },
  "steps": [
    {
      "text": "Request identity, title, body, publisher for the explicit collection, filters and bounded cursor.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        }
      }
    },
    {
      "text": "本人 pending/历史或 实例所有者 发布历史",
      "kind": "product",
      "entities": [
        {
          "entity": "notification",
          "effect": "reads",
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
          ]
        }
      ],
      "contexts": {
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

# Browse notifications owner primary

## Trigger

Request identity, title, body, publisher for the explicit collection, filters and bounded cursor.

## Outcome

本人 pending/历史或 Owner 发布历史

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
- Reading does not acknowledge. Publisher cannot acknowledge their own notice. Expired and withdrawn history remain. Expiry is calculated; reenable resets receive-after. Published title/body cannot be edited.
