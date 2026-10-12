---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ca": "Ca entry"
  },
  "steps": [
    {
      "text": "Request identity, kind, source, target for the explicit selected object.",
      "kind": "actor",
      "actor": "reader",
      "entities": [],
      "contexts": {
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      }
    },
    {
      "text": "一个双端可见 关系",
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
        }
      },
      "actor": "reader"
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
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Read relation primary

## Trigger

Request identity, kind, source, target for the explicit selected object.

## Outcome

一个双端可见 Relation

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Both endpoint versions and visibility are checked separately. Self or cross-Workspace relationships fail. Parent cycles and more than 1,000 checked objects fail without a new relation. Only related normalizes endpoints.
