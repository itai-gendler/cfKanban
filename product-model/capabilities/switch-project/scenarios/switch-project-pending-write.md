---
{
  "kind": "validation",
  "routes": {
    "b": "B entry"
  },
  "steps": [
    {
      "text": "Explicitly select a different verified target.",
      "kind": "actor",
      "actor": "reader",
      "entities": [],
      "contexts": {
        "b": {
          "place": "workbench-web::connection-selection"
        }
      }
    },
    {
      "text": "未解决写入阻止重新绑定/新变更",
      "kind": "product",
      "entities": [],
      "contexts": {
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

# Switch project pending write

## Trigger

Explicitly select a different verified target.

## Outcome

未解决写入阻止重新绑定/新变更

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Failed explicit instance/identity verification makes no new binding. Pending writes block new mutation or rebind. Shared task views do not promise full host lifecycle parity.
