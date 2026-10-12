---
{
  "kind": "primary",
  "routes": {
    "wp": "Wp entry",
    "rp": "Rp entry"
  },
  "steps": [
    {
      "text": "Present the delivered one-time code for its resolved entry.",
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
      "text": "Consume the matched one-time offer and establish its source-bound browser identity.",
      "kind": "product",
      "entities": [
        {
          "entity": "browser-launch",
          "effect": "changes",
          "facts": [
            "Consumed at"
          ],
          "from": "Available",
          "to": "Consumed"
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

# Open web session primary

## Trigger

Present the delivered one-time code for its resolved entry.

## Outcome

Consume the matched launch once, establish its source-bound Session and carry the browser to the resolved entry.

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Launch is one-time for five minutes and rechecks source and target. Browser lifetime is eight hours, absolute cap seven days and renewal interval thirty minutes. Not-due renewal is a no-op; fixed scope is not expanded.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- Invalid submitted code, consumed/revoked/expired offer or invalidated issuing source produces the structured failure. A supplied authenticated identity must still match the operation's current-source and target contract; full recovery retains the original identity and Passkeys, while rotation replaces only its authenticating Credential.

- Non-Owner exchange establishes project_selection and retains the initial entry; Owner retains its target. Revoked source Credential or lost target access returns unavailable. Matching committed replay reports cookie_available=false and redelivers no Session/CSRF secret.
