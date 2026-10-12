---
{
  "kind": "primary",
  "routes": {
    "wo": "Wo entry",
    "ra": "Ra entry"
  },
  "steps": [
    {
      "text": "Request the current browser authentication state, resolved target and live allowed scope.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wo": {
          "place": "online-web::administration::instance"
        },
        "ra": {
          "place": "rest-api::authenticated"
        }
      }
    },
    {
      "text": "核验 实例所有者 target/allowed scope",
      "kind": "product",
      "entities": [
        {
          "entity": "web-session",
          "effect": "reads",
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
          ]
        }
      ],
      "contexts": {
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

# Read web session owner

## Trigger

Request the current browser authentication state, resolved target and live allowed scope.

## Outcome

核验 Owner target/allowed scope

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Launch is one-time for five minutes and rechecks source and target. Browser lifetime is eight hours, absolute cap seven days and renewal interval thirty minutes. Not-due renewal is a no-op; fixed scope is not expanded.

- A different sessionId for the same identity cannot substitute for the selected current Cookie. Revoked/expired Session or source is refused. Renewal preserves source and target and rechecks current target authorization; it never expands fixed scope.
