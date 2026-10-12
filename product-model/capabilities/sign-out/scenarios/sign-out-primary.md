---
{
  "kind": "primary",
  "routes": {
    "wa": "Wa entry",
    "ra": "Ra entry"
  },
  "steps": [
    {
      "text": "Request revoking the current browser identity under its CSRF contract.",
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
      "text": "撤销当前 Session、清除 Cookie",
      "kind": "product",
      "entities": [
        {
          "entity": "web-session",
          "effect": "changes",
          "facts": [
            "Revoked at",
            "Version"
          ],
          "from": "Active",
          "to": "Revoked"
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
      "target": "apps/worker/src/services/web-auth.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Sign out primary

## Trigger

Request revoking the current browser identity under its CSRF contract.

## Outcome

撤销当前 Session、清除 Cookie

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Launch is one-time for five minutes and rechecks source and target. Browser lifetime is eight hours, absolute cap seven days and renewal interval thirty minutes. Not-due renewal is a no-op; fixed scope is not expanded.
- This operation retains the csrf contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- The browser operation retains its source, challenge and CSRF contract. A lost response alone does not prove success or failure; the endpoint's actual confirmation remains authoritative.
