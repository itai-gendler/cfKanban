---
{
  "kind": "primary",
  "routes": {
    "wo": "Wo entry"
  },
  "steps": [
    {
      "text": "Request service discovery; authenticated entry also reads the current identity and live visible scope.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wo": {
          "place": "online-web::administration::instance"
        }
      }
    },
    {
      "text": "公开发现；认证路径另读本人及 visible scope",
      "kind": "product",
      "entities": [
        {
          "entity": "instance",
          "effect": "reads",
          "facts": [
            "Identity",
            "Service version",
            "Schema version",
            "Discovery version",
            "Observed origin",
            "Preferred origin",
            "Origin version",
            "Advertised capabilities",
            "Release version"
          ]
        },
        {
          "entity": "project",
          "effect": "reads",
          "facts": [
            "Identity",
            "Name"
          ]
        },
        {
          "entity": "workspace",
          "effect": "reads",
          "facts": [
            "Identity",
            "Name"
          ]
        },
        {
          "entity": "principal",
          "effect": "reads",
          "facts": [
            "Identity",
            "Display name"
          ]
        }
      ],
      "contexts": {
        "wo": {
          "place": "online-web::administration::instance"
        }
      },
      "actor": "owner"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/identity.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Browse instance owner primary

## Trigger

Request public instance discovery; authenticated entry also reads the current identity and live visible scope.

## Outcome

公开发现；认证路径另读本人及 visible scope

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
- Authenticated visible-scope projection returns target IDs, display names and effective role; it is not a direct-access history inventory.
