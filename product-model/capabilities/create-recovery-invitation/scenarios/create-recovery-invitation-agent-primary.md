---
{
  "kind": "primary",
  "routes": {
    "ro": "Ro entry",
    "co": "Co entry",
    "so": "So entry"
  },
  "steps": [
    {
      "text": "选择非实例所有者的稳定身份，并在创建一次性恢复邀请时确定 full_recovery 或 rotation 模式。",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        },
        "so": {
          "place": "agent-skills::administration"
        }
      }
    },
    {
      "text": "绑定非 实例所有者 稳定身份 的恢复邀请",
      "kind": "product",
      "entities": [
        {
          "entity": "recovery-invitation",
          "effect": "creates",
          "facts": [
            "Identity",
            "Bound principal",
            "Recovery mode",
            "Issuer",
            "Expires at",
            "Version",
            "Redeemed at",
            "Redeemed by",
            "Revoked at",
            "Revoked by",
            "Code digest"
          ],
          "to": "Available"
        }
      ],
      "contexts": {
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
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

# Create recovery invitation agent primary

## Trigger

Select the stable non-owner identity and choose full_recovery or rotation when creating the one-time recovery offer.

## Outcome

绑定非 Owner Principal 的恢复邀请

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Preview does not consume. Expired, revoked, consumed or invalidated-source offers fail without a second redemption. Recovery retains stable identity, grants, history and Passkeys. Remote commit can precede pending local promotion.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
