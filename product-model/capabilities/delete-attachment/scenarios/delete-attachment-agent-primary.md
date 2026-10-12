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
      "text": "Confirm Ready soft deletion or Pending cancellation with the selected reservation's current version.",
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
      "text": "Ready 软删除或 Pending 取消",
      "kind": "product",
      "entities": [
        {
          "entity": "attachment",
          "effect": "changes",
          "facts": [
            "Deleted at",
            "Deleted by",
            "Version"
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
      "target": "apps/worker/src/services/attachments.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Delete attachment agent primary

## Trigger

Confirm Ready soft deletion or Pending cancellation with the selected reservation's current version.

## Outcome

Ready 软删除或 Pending 取消

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Storage availability differs from metadata availability. Size is one byte through 10 MiB, actual digest/size must match, at most twenty active/pending slots and reserved-byte capacity apply. Pending cancellation is not Ready restoration. Soft deletion does not immediately release budget.
- This operation retains the idempotent-cas-delete contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- On agent-skills::authenticated, Pending 取消不可按 Ready 恢复; affected saved facts: changes attachment [Availability, Deleted at, Deleted by, Version].
