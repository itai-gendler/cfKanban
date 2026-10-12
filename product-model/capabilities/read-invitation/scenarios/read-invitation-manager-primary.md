---
{
  "kind": "primary",
  "routes": {
    "wa": "Wa entry",
    "ra": "Ra entry",
    "ca": "Ca entry"
  },
  "steps": [
    {
      "text": "Present the one-time link for non-consuming preview, or select an invitation ID for management detail.",
      "kind": "actor",
      "actor": "project-administrator",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::authenticated-invitation"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      }
    },
    {
      "text": "预览或管理详情，不消费",
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
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::authenticated-invitation"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      },
      "actor": "project-administrator"
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

# Read invitation manager primary

## Trigger

Present the one-time link for non-consuming preview, or select an invitation ID for management detail.

## Outcome

预览或管理详情，不消费

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Holder preview does not consume. Unknown, expired, revoked, consumed or invalidated-issuer offers return refusal without successful preview metadata. Authenticated management history is a different operation and may report retained invalid states. Recovery retains stable identity, grants, history and Passkeys. Remote commit can precede pending local promotion.

- A matched recovery preview returns its bound identity, mode, expiry and recovery warning without consumption. Ordinary target/role preview and recovery preview retain their distinct payloads.
