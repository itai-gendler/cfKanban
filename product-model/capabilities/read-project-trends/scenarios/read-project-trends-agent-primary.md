---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ca": "Ca entry",
    "sa": "Sa entry",
    "m": "M entry"
  },
  "steps": [
    {
      "text": "请求指定项目的 UTC 日期窗口，可附加同项目里程碑过滤。",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "sa": {
          "place": "agent-skills::authenticated"
        },
        "m": {
          "place": "mcp"
        }
      }
    },
    {
      "text": "项目 UTC 趋势及覆盖信息",
      "kind": "product",
      "entities": [
        {
          "entity": "project",
          "effect": "reads",
          "facts": [
            "Trend history",
            "Trend coverage"
          ]
        }
      ],
      "contexts": {
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "sa": {
          "place": "agent-skills::authenticated"
        },
        "m": {
          "place": "mcp"
        }
      },
      "actor": "ai-agent"
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

# Read project trends agent primary

## Trigger

Request the selected child container’s UTC daily window and optional milestone filter.

## Outcome

Project UTC 趋势及覆盖信息

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- UTC history defaults to thirty and is capped at 365 days. Unknown history is null and the current day is partial. Disabled trends and Issue-bound browser scopes are refused. Workspace aggregation refuses more than one hundred active Projects.

- On agent-skills::authenticated, mcp, 未知历史 null，当前日 partial; affected saved facts: reads project [Trend history, Trend coverage].
