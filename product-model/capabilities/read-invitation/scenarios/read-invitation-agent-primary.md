---
{
  "kind": "primary",
  "routes": {
    "rp": "Rp entry",
    "ra": "Ra entry",
    "ro": "Ro entry",
    "ca": "Ca entry",
    "co": "Co entry",
    "sa": "Sa entry",
    "so": "So entry"
  },
  "steps": [
    {
      "text": "Present the one-time link for non-consuming preview, or select an invitation ID for management detail.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "rp": {
          "place": "rest-api::public"
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
        },
        "sa": {
          "place": "agent-skills::authenticated"
        },
        "so": {
          "place": "agent-skills::administration"
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
            "Project targets",
            "Roles",
            "Expires at"
          ]
        }
      ],
      "contexts": {
        "rp": {
          "place": "rest-api::public"
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
        },
        "sa": {
          "place": "agent-skills::authenticated"
        },
        "so": {
          "place": "agent-skills::administration"
        }
      },
      "actor": "ai-agent"
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

# Read invitation agent primary

## Trigger

Present the one-time link for non-consuming preview, or select an invitation ID for management detail.

## Outcome

预览或管理详情，不消费

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Holder preview does not consume. Unknown, expired, revoked, consumed or invalidated-issuer offers return refusal without successful preview metadata. Authenticated management history is a different operation and may report retained invalid states. Recovery retains stable identity, grants, history and Passkeys. Remote commit can precede pending local promotion.

- A matched recovery preview returns its bound identity, mode, expiry and recovery warning without consumption. Ordinary target/role preview and recovery preview retain their distinct payloads.
- A selected recovery offer’s preview returns bound identity, saved recovery mode and expiry; its management/history projection also returns ID, version, redemption and revocation fields. Ordinary target filtering excludes recovery records. Raw digests and plaintext codes are not inventory fields.
