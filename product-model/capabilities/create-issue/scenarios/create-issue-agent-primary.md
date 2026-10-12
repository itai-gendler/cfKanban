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
      "text": "Submit title, optional body and supported non-Done initial status.",
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
      "text": "新 事项，非 Done 初态",
      "kind": "product",
      "entities": [
        {
          "entity": "issue",
          "effect": "creates",
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
          ],
          "to": "Backlog"
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

# Create issue agent primary

## Trigger

Submit title, optional body and a non-Done initial state.

## Outcome

新 Issue，非 Done 初态

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Ordinary creation or editing into Done is refused; completion remains its own operation.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
