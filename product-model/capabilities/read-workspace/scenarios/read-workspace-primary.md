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
      "text": "Request identity, name, description, created at for the explicit selected object.",
      "kind": "actor",
      "actor": "reader",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::workspace"
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
      "text": "一个 工作区 的资料",
      "kind": "product",
      "entities": [
        {
          "entity": "workspace",
          "effect": "reads",
          "facts": [
            "Identity",
            "Name",
            "Description",
            "Created at",
            "Updated at",
            "Version",
            "Archived at",
            "Archived by"
          ]
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::workspace"
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
      "target": "apps/worker/src/services/containers.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Read workspace primary

## Trigger

Request identity, name, description, created at for the explicit selected object.

## Outcome

一个 Workspace 的资料

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
