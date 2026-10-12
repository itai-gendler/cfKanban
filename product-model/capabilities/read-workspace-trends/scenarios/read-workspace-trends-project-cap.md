---
{
  "kind": "edge",
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
      "text": "超过 100 active 项目 不伪造完整结果",
      "kind": "product",
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

# Read workspace trends project cap

## Trigger

Request the selected container’s complete active-child UTC daily window.

## Outcome

too_many_trend_projects is returned before aggregate history is read; no incomplete trend result is disclosed.

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- UTC history defaults to thirty and is capped at 365 days. Unknown history is null and the current day is partial. Disabled trends and Issue-bound browser scopes are refused. Workspace aggregation refuses more than one hundred active Projects.
