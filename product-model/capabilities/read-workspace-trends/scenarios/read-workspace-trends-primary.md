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
      "text": "Request the selected container’s complete active-child UTC daily window.",
      "kind": "actor",
      "actor": "workspace-administrator",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::workspace"
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
      "text": "工作区 全部 active 项目 的聚合趋势",
      "kind": "product",
      "entities": [
        {
          "entity": "workspace",
          "effect": "reads",
          "facts": [
            "Trend history",
            "Trend coverage"
          ]
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::workspace"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      },
      "actor": "workspace-administrator"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/issue-trends.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    }
  ]
}
---

# Read workspace trends primary

## Trigger

Request the selected container’s complete active-child UTC daily window.

## Outcome

Workspace 全部 active Projects 的聚合趋势

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- UTC history defaults to thirty and is capped at 365 days. Unknown history is null and the current day is partial. Disabled trends and Issue-bound browser scopes are refused. Workspace aggregation refuses more than one hundred active Projects.
