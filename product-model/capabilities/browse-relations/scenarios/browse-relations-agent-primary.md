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
      "text": "Request identity, kind, source, target for the explicit collection, filters and bounded cursor.",
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
      "text": "双端可见的 关系 页",
      "kind": "product",
      "entities": [
        {
          "entity": "relation",
          "effect": "reads",
          "facts": [
            "Identity",
            "Kind",
            "Source",
            "Target",
            "Source version",
            "Target version",
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
      "target": "apps/worker/src/services/relations.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    }
  ]
}
---

# Browse relations agent primary

## Trigger

Request identity, kind, source, target for the explicit collection, filters and bounded cursor.

## Outcome

双端可见的 Relation 页

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
- Both endpoint versions and visibility are checked separately. Self or cross-Workspace relationships fail. Parent cycles and more than 1,000 checked objects fail without a new relation. Only related normalizes endpoints.
