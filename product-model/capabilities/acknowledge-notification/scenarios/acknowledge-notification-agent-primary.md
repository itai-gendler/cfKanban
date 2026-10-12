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
      "text": "Explicitly confirm the selected notice.",
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
      "text": "本人显式确认他人公告",
      "kind": "product",
      "entities": [
        {
          "entity": "notification-acknowledgement",
          "effect": "creates",
          "facts": [
            "Notification",
            "Principal",
            "Acknowledged at"
          ]
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

# Acknowledge notification agent primary

## Trigger

Explicitly confirm a selected notice.

## Outcome

本人显式确认他人公告

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Reading does not acknowledge. Publisher cannot acknowledge their own notice. Expired and withdrawn history remain. Expiry is calculated; reenable resets receive-after. Published title/body cannot be edited.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- On agent-skills::authenticated, 发布者不能确认本人公告; this boundary adds no confirmed saved mutation.
- Repeated acknowledgement preserves the first timestamp and single acknowledgement record. A new request key can produce a security event; replay of the same committed request does not repeat the commit. Historical expired or withdrawn notices remain explicitly acknowledgeable when the selected notice is from another publisher.
