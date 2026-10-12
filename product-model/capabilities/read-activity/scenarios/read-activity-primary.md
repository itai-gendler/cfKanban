---
{
  "kind": "primary",
  "routes": {
    "wa": "Wa entry",
    "ra": "Ra entry",
    "ca": "Ca entry"
  },
  "steps": [
    {
      "text": "Request the selected work scope’s domain activity with its supported stream cursor.",
      "kind": "actor",
      "actor": "reader",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
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
        "wa": {
          "place": "online-web::authenticated::project"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      },
      "actor": "reader"
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

# Read activity primary

## Trigger

Request the selected work scope’s domain activity with its supported stream cursor.

## Outcome

当前范围领域活动

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
