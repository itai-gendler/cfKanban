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
      "text": "Request one-time invitation history with the optional target filter and bound cursor.",
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
      "text": "当前管理范围的邀请历史",
      "kind": "product",
      "entities": [
        {
          "entity": "project-invitation",
          "effect": "reads",
          "facts": [
            "Identity",
            "Project targets",
            "Roles",
            "Expires at",
            "Version",
            "Redeemed at",
            "Redeemed by",
            "Revoked at"
          ]
        },
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

# Browse invitations owner primary

## Trigger

Request one-time invitation history with the optional target filter and bound cursor.

## Outcome

当前管理范围的邀请历史

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
- Preview does not consume. Expired, revoked, consumed or invalidated-source offers fail without a second redemption. Recovery retains stable identity, grants, history and Passkeys. Remote commit can precede pending local promotion.
- Recovery history retains the bound identity and the saved full_recovery or rotation mode. A target-filtered ordinary-access history page omits recovery offers.
