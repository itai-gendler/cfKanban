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
      "text": "Present the one-time link for non-consuming preview, or select an invitation ID for management detail.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wo": {
          "place": "online-web::administration::invitations"
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
      "text": "Return the selected recovery offer’s management detail without consuming its code.",
      "kind": "product",
      "entities": [
        {
          "entity": "recovery-invitation",
          "effect": "reads",
          "facts": [
            "Identity",
            "Bound principal",
            "Recovery mode",
            "Expires at",
            "Version",
            "Redeemed at",
            "Redeemed by",
            "Revoked at"
          ]
        }
      ],
      "contexts": {
        "wo": {
          "place": "online-web::administration::invitations"
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
      "target": "apps/worker/src/services/invitations.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Read invitation owner primary

## Trigger

Present the one-time link for non-consuming preview, or select an invitation ID for management detail.

## Outcome

预览或管理详情，不消费

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Holder preview does not consume. Unknown, expired, revoked, consumed or invalidated-issuer offers return refusal without successful preview metadata. Authenticated management history is a different operation and may report retained invalid states. Recovery retains stable identity, grants, history and Passkeys. Remote commit can precede pending local promotion.

- A matched recovery preview returns its bound identity, mode, expiry and recovery warning without consumption. Ordinary target/role preview and recovery preview retain their distinct payloads.
- Recovery history retains the bound identity and the saved full_recovery or rotation mode. A target-filtered ordinary-access history page omits recovery offers.
