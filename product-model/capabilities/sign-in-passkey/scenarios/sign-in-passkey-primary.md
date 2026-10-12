---
{
  "kind": "primary",
  "routes": {
    "wp": "Wp entry",
    "rp": "Rp entry"
  },
  "steps": [
    {
      "text": "Complete the browser authenticator sign-in challenge.",
      "kind": "actor",
      "actor": "visitor",
      "entities": [],
      "contexts": {
        "wp": {
          "place": "online-web::public::launch-exchange"
        },
        "rp": {
          "place": "rest-api::public"
        }
      }
    },
    {
      "text": "通行密钥 登录建立 Session",
      "kind": "product",
      "entities": [
        {
          "entity": "passkey",
          "effect": "reads",
          "facts": []
        },
        {
          "entity": "web-session",
          "effect": "creates",
          "facts": [
            "Identity",
            "Principal",
            "Authentication source",
            "Target",
            "Allowed scope",
            "Entry",
            "Created at",
            "Activity at",
            "Expires at",
            "Absolute expiry",
            "Version",
            "Revoked at"
          ],
          "to": "Active"
        }
      ],
      "contexts": {
        "wp": {
          "place": "online-web::public::launch-exchange"
        },
        "rp": {
          "place": "rest-api::public"
        }
      },
      "actor": "visitor"
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

# Sign in passkey primary

## Trigger

Complete the browser authenticator sign-in challenge.

## Outcome

Passkey 登录建立 Session

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Challenge and source are rechecked. Registration requires a Credential-sourced browser identity; self inventory and revocation also support bearer. Recovery retains saved authenticators.
- This operation retains the write; idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- The browser operation retains its source, challenge and CSRF contract. A lost response alone does not prove success or failure; the endpoint's actual confirmation remains authoritative.
