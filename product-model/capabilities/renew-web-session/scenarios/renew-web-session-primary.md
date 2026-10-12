---
{
  "kind": "primary",
  "routes": {
    "wa": "Wa entry",
    "ra": "Ra entry"
  },
  "steps": [
    {
      "text": "Request renewing the current browser identity under its source and CSRF contract.",
      "kind": "actor",
      "actor": "participant",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project-selection"
        },
        "ra": {
          "place": "rest-api::authenticated"
        }
      }
    },
    {
      "text": "合法续期或 no-op",
      "kind": "product",
      "entities": [
        {
          "entity": "web-session",
          "effect": "changes",
          "facts": [
            "Expires at",
            "Activity at",
            "Version"
          ]
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project-selection"
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

# Renew web session primary

## Trigger

Request renewing the current browser identity under its source and CSRF contract.

## Outcome

合法续期或 no-op

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Launch is one-time for five minutes and rechecks source and target. Browser lifetime is eight hours, absolute cap seven days and renewal interval thirty minutes. Not-due renewal is a no-op; fixed scope is not expanded.
- This operation retains the csrf-idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- The browser operation retains its source, challenge and CSRF contract. A lost response alone does not prove success or failure; the endpoint's actual confirmation remains authoritative.

- A different sessionId for the same identity cannot substitute for the selected current Cookie. Revoked/expired Session or source is refused. Renewal preserves source and target and rechecks current target authorization; it never expands fixed scope.
