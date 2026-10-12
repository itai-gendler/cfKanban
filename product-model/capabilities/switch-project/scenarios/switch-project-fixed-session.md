---
{
  "kind": "validation",
  "routes": {
    "wa": "Wa entry",
    "wo": "Wo entry"
  },
  "steps": [
    {
      "text": "Explicitly select a different verified target.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project-selection"
        },
        "wo": {
          "place": "online-web::administration::instance"
        }
      }
    },
    {
      "text": "不扩大固定 scope",
      "kind": "product",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project-selection"
        },
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

# Switch project fixed session

## Trigger

Explicitly select a different verified target.

## Outcome

不扩大固定 scope

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Failed explicit instance/identity verification makes no new binding. Pending writes block new mutation or rebind. Shared task views do not promise full host lifecycle parity.
