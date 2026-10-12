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
      "text": "Submit name and marker.",
      "kind": "actor",
      "actor": "writer",
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
      "text": "新 标签",
      "kind": "product",
      "entities": [
        {
          "entity": "label",
          "effect": "creates",
          "facts": [
            "Identity",
            "Name",
            "Marker",
            "Version",
            "Deleted at",
            "Deleted by"
          ],
          "to": "Active"
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
      "actor": "writer"
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

# Create label primary

## Trigger

Submit name, marker for the selected target with the required current version.

## Outcome

新 Label

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Associations require a same-Project active definition and at most twenty stored associations; deleted definitions keep associations and their count. Removing an association never deletes its definition.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
