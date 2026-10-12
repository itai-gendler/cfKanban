---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ca": "Ca entry"
  },
  "steps": [
    {
      "text": "Request or present a one-time launch for an explicit target.",
      "kind": "actor",
      "actor": "participant",
      "entities": [],
      "contexts": {
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      }
    },
    {
      "text": "Create and securely deliver the source-bound one-time launch; browser redemption continues the same process.",
      "kind": "product",
      "entities": [
        {
          "entity": "browser-launch",
          "effect": "creates",
          "facts": [
            "Identity",
            "Source credential",
            "Principal",
            "Target",
            "Expires at",
            "Consumed at",
            "Code digest",
            "Revoked at"
          ],
          "to": "Available"
        }
      ],
      "contexts": {
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
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

# Open web session authenticated

## Trigger

Request or present a one-time launch for an explicit target.

## Outcome

Create and securely deliver the source-bound one-time launch; browser redemption continues the same process.

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Launch is one-time for five minutes and rechecks source and target. Browser lifetime is eight hours, absolute cap seven days and renewal interval thirty minutes. Not-due renewal is a no-op; fixed scope is not expanded.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- Invalid submitted code, consumed/revoked/expired offer or invalidated issuing source produces the structured failure. A supplied authenticated identity must still match the operation's current-source and target contract; full recovery retains the original identity and Passkeys, while rotation replaces only its authenticating Credential.

- Non-Owner exchange establishes project_selection and retains the initial entry; Owner retains its target. Revoked source Credential or lost target access returns unavailable. Matching committed replay reports cookie_available=false and redelivers no Session/CSRF secret.
