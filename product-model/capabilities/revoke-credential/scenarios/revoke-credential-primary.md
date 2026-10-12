---
{
  "kind": "primary",
  "routes": {
    "wo": "Wo entry",
    "ro": "Ro entry",
    "co": "Co entry"
  },
  "steps": [
    {
      "text": "Request revoking the explicitly selected source of an ordinary identity at its current version.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wo": {
          "place": "online-web::administration::access"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        }
      }
    },
    {
      "text": "撤销非 实例所有者 稳定身份 的 凭据",
      "kind": "product",
      "entities": [
        {
          "entity": "credential",
          "effect": "changes",
          "facts": [
            "Revoked at",
            "Revocation reason",
            "Version"
          ],
          "from": "Active",
          "to": "Revoked"
        }
      ],
      "contexts": {
        "wo": {
          "place": "online-web::administration::access"
        },
        "ro": {
          "place": "rest-api::administration"
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
      "target": "apps/worker/src/services/access.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Revoke credential primary

## Trigger

Request revoking the explicitly selected non-Owner source at its current version.

## Outcome

撤销非 Owner Principal 的 Credential

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- This operation retains the cas-delete contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
