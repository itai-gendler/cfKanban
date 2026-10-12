---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ca": "Ca entry"
  },
  "steps": [
    {
      "text": "Request identity, name, marker, version for the explicit selected object.",
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
      "text": "一个 标签",
      "kind": "product",
      "entities": [
        {
          "entity": "label",
          "effect": "reads",
          "facts": [
            "Identity",
            "Name",
            "Marker",
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
      "target": "apps/worker/src/services/labels.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Read label primary

## Trigger

Request identity, name, marker, version for the explicit selected object.

## Outcome

一个 Label

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Associations require a same-Project active definition and at most twenty stored associations; deleted definitions keep associations and their count. Removing an association never deletes its definition.
