---
{
  "kind": "primary",
  "routes": {
    "wa": "Wa entry",
    "b": "B entry",
    "ra": "Ra entry",
    "ca": "Ca entry"
  },
  "steps": [
    {
      "text": "Request the five fixed workflow keys and their current display names for the selected container.",
      "kind": "actor",
      "actor": "reader",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project"
        },
        "b": {
          "place": "workbench-web::project"
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
      "text": "五个固定状态的当前名称",
      "kind": "product",
      "entities": [
        {
          "entity": "project-status-name",
          "effect": "reads",
          "facts": [
            "Project",
            "Status key",
            "Display name",
            "Category",
            "Position",
            "Terminal",
            "Project version"
          ]
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project"
        },
        "b": {
          "place": "workbench-web::project"
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
      "target": "apps/worker/src/services/containers.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    }
  ]
}
---

# Browse project status names primary

## Trigger

Request the five fixed workflow keys and their current display names for the selected container.

## Outcome

五个固定状态的当前名称

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
