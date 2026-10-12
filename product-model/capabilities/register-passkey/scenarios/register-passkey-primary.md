---
{
  "kind": "primary",
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
      "text": "浏览器注册本人 通行密钥",
      "kind": "product",
      "entities": [
        {
          "entity": "passkey",
          "effect": "creates",
          "facts": [
            "Identity",
            "Principal",
            "Authenticator description",
            "Created at",
            "Last used at",
            "Version",
            "Revoked at"
          ],
          "to": "Active"
        }
      ],
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

# Register passkey primary

## Trigger

Complete the browser registration challenge.

## Outcome

浏览器注册本人 Passkey

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Challenge and source are rechecked. Registration requires a Credential-sourced browser identity; self inventory and revocation also support bearer. Recovery retains saved authenticators.
- This operation retains the csrf; csrf-idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- The browser operation retains its source, challenge and CSRF contract. A lost response alone does not prove success or failure; the endpoint's actual confirmation remains authoritative.
