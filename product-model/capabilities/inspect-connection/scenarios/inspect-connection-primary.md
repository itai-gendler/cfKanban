---
{
  "kind": "primary",
  "routes": {
    "b": "B entry",
    "ca": "Ca entry"
  },
  "steps": [
    {
      "text": "List nonsecret candidates and explicitly select the connection to verify.",
      "kind": "actor",
      "actor": "participant",
      "entities": [],
      "contexts": {
        "b": {
          "place": "workbench-web::connection-selection"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      }
    },
    {
      "text": "非秘密候选；选择后核验身份",
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
        }
      ],
      "contexts": {
        "b": {
          "place": "workbench-web::connection-selection"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      },
      "actor": "participant"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/runtime.mjs"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    }
  ]
}
---

# Inspect connection primary

## Trigger

List nonsecret candidates and explicitly select the connection to verify.

## Outcome

非秘密候选；选择后核验身份

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Failed explicit instance/identity verification makes no new binding. Pending writes block new mutation or rebind. Shared task views do not promise full host lifecycle parity.
