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
      "text": "Choose an eligible stable identity with the current work-item version.",
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
      "text": "设置合格 稳定身份，包括 assign-to-me 路径",
      "kind": "product",
      "entities": [
        {
          "entity": "issue",
          "effect": "changes",
          "facts": [
            "Assignee",
            "Version",
            "Updated at"
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

# Assign issue agent primary

## Trigger

Choose an eligible stable identity with the current work-item version.

## Outcome

设置合格 Principal，包括 assign-to-me 路径

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- An ineligible identity is refused as a new target; the former assignee stays in history. Assignment changes no exclusivity or workflow status.
- This operation retains the cas; idempotent-cas contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- On agent-skills::authenticated, mcp, 旧身份保留但不能重新作为合格目标; affected saved facts: reads issue [Assignee, Version, Updated at].

- On agent-skills::authenticated, 只改变指派；不宣称 MCP 有专用 assign-me; affected saved facts: changes issue [Assignee, Version, Updated at].
