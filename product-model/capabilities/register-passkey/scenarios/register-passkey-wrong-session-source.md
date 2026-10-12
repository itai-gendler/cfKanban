---
{
  "kind": "validation",
  "routes": {
    "wa": "Wa entry",
    "ra": "Ra entry"
  },
  "steps": [
    {
      "text": "Complete the browser registration challenge.",
      "kind": "actor",
      "actor": "participant",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::profile"
        },
        "ra": {
          "place": "rest-api::authenticated"
        }
      }
    },
    {
      "text": "通行密钥-sourced Session 不能注册新 通行密钥",
      "kind": "product",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::profile"
        },
        "ra": {
          "place": "rest-api::authenticated"
        }
      },
      "actor": "participant"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/passkeys.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Register passkey wrong session source

## Trigger

Complete the browser registration challenge.

## Outcome

Passkey-sourced Session 不能注册新 Passkey

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Challenge and source are rechecked. Registration requires a Credential-sourced browser identity; self inventory and revocation also support bearer. Recovery retains saved authenticators.
- This operation retains the csrf; csrf-idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- The browser operation retains its source, challenge and CSRF contract. A lost response alone does not prove success or failure; the endpoint's actual confirmation remains authoritative.
