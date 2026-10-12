---
{
  "kind": "primary",
  "routes": {
    "m": "M entry"
  },
  "steps": [
    {
      "text": "Request a thread or global view for the explicit verified target.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "m": {
          "place": "mcp"
        }
      }
    },
    {
      "text": "Agent 请求并取得核验目标的工作台视图引用",
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
            "Advertised capabilities"
          ]
        },
        {
          "entity": "principal",
          "effect": "reads",
          "facts": [
            "Identity",
            "Display name"
          ]
        },
        {
          "entity": "project",
          "effect": "reads",
          "facts": [
            "Identity",
            "Name"
          ]
        }
      ],
      "contexts": {
        "m": {
          "place": "mcp"
        }
      },
      "actor": "ai-agent"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/mcp/src/workbench.mjs"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Open workbench agent primary

## Trigger

Request a thread or global view for the explicit verified target.

## Outcome

Agent 请求并取得核验目标的工作台视图引用

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Failed explicit instance/identity verification makes no new binding. Pending writes block new mutation or rebind. Shared task views do not promise full host lifecycle parity.
