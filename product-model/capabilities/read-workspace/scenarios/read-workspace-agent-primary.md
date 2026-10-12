---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ro": "Ro entry",
    "ca": "Ca entry",
    "co": "Co entry",
    "sa": "Sa entry",
    "so": "So entry"
  },
  "steps": [
    {
      "text": "Request identity, name, description, created at for the explicit selected object.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "co": {
          "place": "public-cli::administration"
        },
        "sa": {
          "place": "agent-skills::authenticated"
        },
        "so": {
          "place": "agent-skills::administration"
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
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "co": {
          "place": "public-cli::administration"
        },
        "sa": {
          "place": "agent-skills::authenticated"
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

# Read workspace agent primary

## Trigger

Request identity, name, description, created at for the explicit selected object.

## Outcome

一个 Workspace 的资料

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
