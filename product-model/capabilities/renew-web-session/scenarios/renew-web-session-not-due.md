---
{
  "kind": "primary",
  "routes": {
    "wa": "Wa entry",
    "wo": "Wo entry",
    "ra": "Ra entry"
  },
  "steps": [
    {
      "text": "Request renewing the current browser identity under its source and CSRF contract.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project-selection"
        },
        "wo": {
          "place": "online-web::administration::instance"
        },
        "ra": {
          "place": "rest-api::authenticated"
        }
      }
    },
    {
      "text": "no-op，不改 Session/追加续期事件",
      "kind": "product",
      "entities": [
        {
          "entity": "web-session",
          "effect": "reads",
          "facts": [
            "Expires at",
            "Absolute expiry",
            "Activity at",
            "Version"
          ]
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project-selection"
        },
        "wo": {
          "place": "online-web::administration::instance"
        },
        "ra": {
          "place": "rest-api::authenticated"
        }
      },
      "actor": "owner"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/web-session-renewal.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Renew web session not due

## Trigger

Request renewing the current browser identity under its source and CSRF contract.

## Outcome

no-op，不改 Session/追加续期事件

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Launch is one-time for five minutes and rechecks source and target. Browser lifetime is eight hours, absolute cap seven days and renewal interval thirty minutes. Not-due renewal is a no-op; fixed scope is not expanded.
- This operation retains the csrf-idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- The browser operation retains its source, challenge and CSRF contract. A lost response alone does not prove success or failure; the endpoint's actual confirmation remains authoritative.

- A different sessionId for the same identity cannot substitute for the selected current Cookie. Revoked/expired Session or source is refused. Renewal preserves source and target and rechecks current target authorization; it never expands fixed scope.
