---
{
  "kind": "primary",
  "routes": {
    "wo": "Wo entry",
    "ro": "Ro entry",
    "co": "Co entry"
  },
  "steps": [
    {
      "text": "Request the service security/domain audit page with its supported filters and stream cursor.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wo": {
          "place": "online-web::administration::audit"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
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
        "wo": {
          "place": "online-web::administration::audit"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        }
      },
      "actor": "owner"
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

# Read audit primary

## Trigger

Request the instance security/domain audit page with its supported filters and stream cursor.

## Outcome

Owner 安全/领域审计

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
