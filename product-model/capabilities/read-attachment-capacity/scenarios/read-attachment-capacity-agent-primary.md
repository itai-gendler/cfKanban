---
{
  "kind": "primary",
  "routes": {
    "ro": "Ro entry",
    "co": "Co entry",
    "so": "So entry"
  },
  "steps": [
    {
      "text": "Request configured, limit, reserved bytes, version for the explicit selected object.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        },
        "so": {
          "place": "agent-skills::administration"
        }
      }
    },
    {
      "text": "当前配置、上限、reserved bytes、版本",
      "kind": "product",
      "entities": [
        {
          "entity": "attachment-capacity",
          "effect": "reads",
          "facts": [
            "Configured",
            "Limit",
            "Reserved bytes",
            "Version"
          ]
        }
      ],
      "contexts": {
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        },
        "so": {
          "place": "agent-skills::administration"
        }
      },
      "actor": "ai-agent"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/attachment-settings.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Read attachment capacity agent primary

## Trigger

Request configured, limit, reserved bytes, version for the explicit selected object.

## Outcome

当前配置、上限、reserved bytes、版本

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Storage availability differs from metadata availability. Size is one byte through 10 MiB, actual digest/size must match, at most twenty active/pending slots and reserved-byte capacity apply. Pending cancellation is not Ready restoration. Soft deletion does not immediately release budget.
