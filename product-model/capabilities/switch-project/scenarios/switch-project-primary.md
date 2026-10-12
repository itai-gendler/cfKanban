---
{
  "kind": "primary",
  "routes": {
    "wa": "Wa entry",
    "b": "B entry"
  },
  "steps": [
    {
      "text": "Explicitly select a different verified target.",
      "kind": "actor",
      "actor": "reader",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project-selection"
        },
        "b": {
          "place": "workbench-web::connection-selection"
        }
      }
    },
    {
      "text": "核验后导航/绑定目标 项目",
      "kind": "product",
      "entities": [
        {
          "entity": "project",
          "effect": "reads",
          "facts": [
            "Identity",
            "Name"
          ]
        },
        {
          "entity": "web-session",
          "effect": "reads",
          "facts": [
            "Target",
            "Allowed scope"
          ]
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project-selection"
        },
        "b": {
          "place": "workbench-web::connection-selection"
        }
      },
      "actor": "reader"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/components/ProjectSwitcher.vue"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Switch project primary

## Trigger

Explicitly select a different verified target.

## Outcome

核验后导航/绑定目标 Project

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Failed explicit instance/identity verification makes no new binding. Pending writes block new mutation or rebind. Shared task views do not promise full host lifecycle parity.
