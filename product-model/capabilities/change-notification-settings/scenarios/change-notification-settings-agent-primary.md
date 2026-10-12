---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ca": "Ca entry",
    "sa": "Sa entry"
  },
  "steps": [
    {
      "text": "Choose the reception setting with its current preference version.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "sa": {
          "place": "agent-skills::authenticated"
        }
      }
    },
    {
      "text": "Disable reception and advance the preference version while preserving the receive-after boundary.",
      "kind": "product",
      "entities": [
        {
          "entity": "notification-preferences",
          "effect": "changes",
          "facts": [
            "Enabled",
            "Version"
          ],
          "from": "Enabled",
          "to": "Disabled"
        }
      ],
      "contexts": {
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "sa": {
          "place": "agent-skills::authenticated"
        }
      },
      "actor": "ai-agent"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/notifications.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Change notification settings agent primary

## Trigger

Choose the reception setting with its current preference version.

## Outcome

保存 enabled/receive-after

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Reading does not acknowledge. Publisher cannot acknowledge their own notice. Expired and withdrawn history remain. Expiry is calculated; reenable resets receive-after. Published title/body cannot be edited.
- This operation retains the idempotent-cas contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- On agent-skills::authenticated, off→on 重设接收起点; affected saved facts: changes notification preferences [Enabled, Receive after, Version].
