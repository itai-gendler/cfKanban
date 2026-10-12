---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ca": "Ca entry",
    "sa": "Sa entry"
  },
  "steps": [
    {
      "text": "Request the selected work scope’s domain activity with its supported stream cursor.",
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
        }
      }
    },
    {
      "text": "当前范围领域活动",
      "kind": "product",
      "entities": [
        {
          "entity": "event",
          "effect": "reads",
          "facts": [
            "Identity",
            "Sequence",
            "Stream",
            "Operation",
            "Actor principal",
            "Actor credential",
            "Authorized via",
            "Workspace",
            "Project",
            "Subject",
            "Payload",
            "Created at"
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
        }
      },
      "actor": "ai-agent"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/events.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Read activity agent primary

## Trigger

Request the selected work scope’s domain activity with its supported stream cursor.

## Outcome

当前范围领域活动

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
