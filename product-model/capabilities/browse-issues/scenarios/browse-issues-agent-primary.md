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
      "text": "Request identity, identifier, title, body for the explicit collection, filters and bounded cursor.",
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
      "text": "明确范围的 事项 页、Board 或候选队列",
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

# Browse issues agent primary

## Trigger

Request identity, identifier, title, body for the explicit collection, filters and bounded cursor.

## Outcome

明确范围的 Issue 页、Board 或候选队列

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
- Hidden neighbours and their counts are omitted. Board columns paginate independently; loaded and has-more never stand in for totals. Ordinary lists use updated-time/number descending; Todo candidates use priority and FIFO.

- On agent-skills::authenticated, mcp, 明确 1–20 Projects，M 使用普通 aggregate list; affected saved facts: reads issue [Identity, Identifier, Title, Body, Status, Priority, Assignee, Manual block reason, Visible blocking, Labels, Milestone, Created at, Updated at, Version, Deleted at, Deleted by].

- On agent-skills::authenticated, Todo 候选，不自动指派; affected saved facts: reads issue [Identity, Identifier, Title, Body, Status, Priority, Assignee, Manual block reason, Visible blocking, Labels, Milestone, Created at, Updated at, Version, Deleted at, Deleted by].

- On agent-skills::authenticated, 保留失权 assignee 的历史身份; affected saved facts: reads issue [Identity, Identifier, Title, Body, Status, Priority, Assignee, Manual block reason, Visible blocking, Labels, Milestone, Created at, Updated at, Version, Deleted at, Deleted by].

- On agent-skills::authenticated, 各状态独立分页，loaded/has_more 不冒充总量; affected saved facts: reads issue [Identity, Identifier, Title, Body, Status, Priority, Assignee, Manual block reason, Visible blocking, Labels, Milestone, Created at, Updated at, Version, Deleted at, Deleted by].

- On agent-skills::authenticated, mcp, 旧游标不能跨过滤、身份/scope 续用；返回游标范围错误，不披露事项结果或写入。

- On agent-skills::authenticated, mcp, 空结果成功; affected saved facts: reads issue [Identity, Identifier, Title, Body, Status, Priority, Assignee, Manual block reason, Visible blocking, Labels, Milestone, Created at, Updated at, Version, Deleted at, Deleted by].

- MCP aggregate listing uses the ordinary explicitly scoped list and exposes no candidates tool; ready-to-claim is not inferred from MCP availability.
