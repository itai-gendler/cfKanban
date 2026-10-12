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
      "text": "Request identity, identifier, title, body for the explicit selected object.",
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
      "text": "事项 详情及对应有界 context/reference",
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

# Read issue agent primary

## Trigger

Request identity, identifier, title, body for the explicit selected object.

## Outcome

Issue 详情及对应有界 context/reference

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Hidden neighbours and their counts are omitted. Board columns paginate independently; loaded and has-more never stand in for totals. Ordinary lists use updated-time/number descending; Todo candidates use priority and FIFO.

- On agent-skills::authenticated, mcp, 不披露隐藏邻接事项和计数; affected saved facts: reads issue [Identity, Identifier, Title, Body, Status, Priority, Assignee, Manual block reason, Visible blocking, Labels, Milestone, Created at, Updated at, Version, Deleted at, Deleted by].

- On agent-skills::authenticated, 删除模式读取及恢复信息，不扩写到 B/M; affected saved facts: reads issue [Identity, Identifier, Title, Body, Status, Priority, Assignee, Manual block reason, Visible blocking, Labels, Milestone, Created at, Updated at, Version, Deleted at, Deleted by].
