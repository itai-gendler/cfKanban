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
      "text": "Request identity, title, description, due date for the explicit collection, filters and bounded cursor.",
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
      "text": "里程碑 页及进度",
      "kind": "product",
      "entities": [
        {
          "entity": "milestone",
          "effect": "reads",
          "facts": [
            "Identity",
            "Title",
            "Description",
            "Due date",
            "Status",
            "Version",
            "Progress"
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
      "target": "apps/worker/src/services/milestones.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    }
  ]
}
---

# Browse milestones agent primary

## Trigger

Request identity, title, description, due date for the explicit collection, filters and bounded cursor.

## Outcome

Milestone 页及进度

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
- Same-Project Closed targets remain associable; closing does not complete work. Progress excludes deleted tasks and separates Done, Canceled and unfinished.

- On agent-skills::authenticated, mcp, Closed 仍可读取; affected saved facts: reads milestone [Identity, Title, Description, Due date, Status, Version, Progress].
