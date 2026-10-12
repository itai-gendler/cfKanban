---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ro": "Ro entry",
    "ca": "Ca entry",
    "co": "Co entry",
    "sa": "Sa entry",
    "so": "So entry"
  },
  "steps": [
    {
      "text": "Request identity, title, body, publisher for the explicit collection, filters and bounded cursor.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "co": {
          "place": "public-cli::administration"
        },
        "sa": {
          "place": "agent-skills::authenticated"
        },
        "so": {
          "place": "agent-skills::administration"
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
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "co": {
          "place": "public-cli::administration"
        },
        "sa": {
          "place": "agent-skills::authenticated"
        },
        "so": {
          "place": "agent-skills::administration"
        }
      },
      "actor": "ai-agent"
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

# Browse notifications agent primary

## Trigger

Request identity, title, body, publisher for the explicit collection, filters and bounded cursor.

## Outcome

本人 pending/历史或 Owner 发布历史

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
- Reading does not acknowledge. Publisher cannot acknowledge their own notice. Expired and withdrawn history remain. Expiry is calculated; reenable resets receive-after. Published title/body cannot be edited.

- On agent-skills::authenticated, 历史保留过期/撤回公告; affected saved facts: reads notification [Identity, Title, Body, Publisher, Published at, Expires at, Withdrawn at, Version, Visible status].
