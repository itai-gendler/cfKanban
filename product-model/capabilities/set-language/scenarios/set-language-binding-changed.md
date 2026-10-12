---
{
  "kind": "edge",
  "routes": {
    "b": "B entry"
  },
  "steps": [
    {
      "text": "Choose en or zh-CN for the explicitly bound identity.",
      "kind": "actor",
      "actor": "participant",
      "entities": [],
      "contexts": {
        "b": {
          "place": "workbench-web::project"
        }
      }
    },
    {
      "text": "The changed local session context blocks a new preference write and retains the original pending operation for recovery.",
      "kind": "product",
      "entities": [],
      "contexts": {
        "b": {
          "place": "workbench-web::project"
        }
      },
      "actor": "participant"
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
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/local-runtime/src/workbench/controller.mjs"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/local-runtime/src/workbench/bridge.mjs"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/App.vue"
    }
  ]
}
---

# Set language binding changed

## Trigger

Choose en or zh-CN for the explicitly bound identity.

## Outcome

A changed local session context prevents a new write or rebind; an earlier in-flight result remains attached to its original identity and may be uncertain.

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- This operation retains the idempotent-cas contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
- An already submitted request may have committed for its original identity. A stale or mismatched response is not applied to a different binding, and original-request recovery is retained rather than asserting rollback.
