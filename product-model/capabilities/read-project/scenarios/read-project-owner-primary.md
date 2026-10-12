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
      "text": "Request identity, name, context, created at for the explicit selected object.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wo": {
          "place": "online-web::administration::containers"
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
      "text": "一个 项目 的资料",
      "kind": "product",
      "entities": [
        {
          "entity": "project",
          "effect": "reads",
          "facts": [
            "Identity",
            "Name",
            "Context",
            "Created at",
            "Updated at",
            "Version",
            "Archived at",
            "Archived by"
          ]
        }
      ],
      "contexts": {
        "wo": {
          "place": "online-web::administration::containers"
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
      "target": "apps/worker/src/services/containers.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    }
  ]
}
---

# Read project owner primary

## Trigger

Request identity, name, context, created at for the explicit selected object.

## Outcome

一个 Project 的资料

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
