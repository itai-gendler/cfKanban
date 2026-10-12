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
      "text": "Request identity, identifier, title, body for the explicit collection, filters and bounded cursor.",
      "kind": "actor",
      "actor": "reader",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::work-list"
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
      "text": "明确 1–20 项目，M 使用普通 aggregate list",
      "kind": "product",
      "entities": [
        {
          "entity": "issue",
          "effect": "reads",
          "facts": [
            "Identity",
            "Identifier",
            "Title",
            "Body",
            "Status",
            "Priority",
            "Assignee",
            "Manual block reason",
            "Visible blocking",
            "Labels",
            "Milestone",
            "Created at",
            "Updated at",
            "Version",
            "Deleted at",
            "Deleted by"
          ]
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::work-list"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      },
      "actor": "reader"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/issues.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    }
  ]
}
---

# Browse issues work list

## Trigger

Request identity, identifier, title, body for the explicit collection, filters and bounded cursor.

## Outcome

明确 1–20 Projects，M 使用普通 aggregate list

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
- Hidden neighbours and their counts are omitted. Board columns paginate independently; loaded and has-more never stand in for totals. Ordinary lists use updated-time/number descending; Todo candidates use priority and FIFO.
