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
      "text": "Request the selected container’s management-source history and page cursor.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wo": {
          "place": "online-web::administration::access"
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
      "text": "本 工作区 管理员清单；候选查询属于任命路径",
      "kind": "product",
      "entities": [
        {
          "entity": "workspace-administrator-grant",
          "effect": "reads",
          "facts": [
            "Identity",
            "Principal",
            "Workspace",
            "Version",
            "Generation",
            "Granted at",
            "Revoked at"
          ]
        }
      ],
      "contexts": {
        "wo": {
          "place": "online-web::administration::access"
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
      "target": "apps/worker/src/services/scoped-administrators.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Browse workspace administrators owner primary

## Trigger

Request the selected container’s management-source history and page cursor.

## Outcome

本 Workspace 管理员清单；候选查询属于任命路径

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
