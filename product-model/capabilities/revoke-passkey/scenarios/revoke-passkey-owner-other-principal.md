---
{
  "kind": "primary",
  "routes": {
    "wa": "Wa entry",
    "wo": "Wo entry",
    "ra": "Ra entry",
    "ro": "Ro entry",
    "ca": "Ca entry",
    "co": "Co entry"
  },
  "steps": [
    {
      "text": "Select the nonsecret authenticator entry and confirm revocation with its current version.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::profile"
        },
        "wo": {
          "place": "online-web::administration::access"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "co": {
          "place": "public-cli::administration"
        }
      }
    },
    {
      "text": "实例所有者 撤销非 实例所有者 目标",
      "kind": "product",
      "entities": [
        {
          "entity": "passkey",
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
          "place": "online-web::authenticated::profile"
        },
        "wo": {
          "place": "online-web::administration::access"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "co": {
          "place": "public-cli::administration"
        }
      },
      "actor": "owner"
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

# Revoke passkey owner other principal

## Trigger

Select the nonsecret authenticator entry and confirm revocation with its current version.

## Outcome

Owner 撤销非 Owner 目标

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Challenge and source are rechecked. Registration requires a Credential-sourced browser identity; self inventory and revocation also support bearer. Recovery retains saved authenticators.
- This operation retains the csrf-idempotent-cas-delete; csrf-cas-delete contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
