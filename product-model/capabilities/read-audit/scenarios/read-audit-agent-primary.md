---
{
  "kind": "primary",
  "routes": {
    "ro": "Ro entry",
    "co": "Co entry",
    "so": "So entry"
  },
  "steps": [
    {
      "text": "Request the service security/domain audit page with its supported filters and stream cursor.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        },
        "so": {
          "place": "agent-skills::administration"
        }
      }
    },
    {
      "text": "实例所有者 安全/领域审计",
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
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        },
        "so": {
          "place": "agent-skills::administration"
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

# Read audit agent primary

## Trigger

Request the instance security/domain audit page with its supported filters and stream cursor.

## Outcome

Owner 安全/领域审计

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
