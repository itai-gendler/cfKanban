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
      "text": "Request identity, name, description, created at for the explicit collection, filters and bounded cursor.",
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
      "text": "当前可见/可管理 工作区 页",
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

# Browse workspaces owner primary

## Trigger

Request identity, name, description, created at for the explicit collection, filters and bounded cursor.

## Outcome

当前可见/可管理 Workspace 页

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
