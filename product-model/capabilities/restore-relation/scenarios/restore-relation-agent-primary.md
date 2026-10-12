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
      "text": "Request restoring the relationship with its own and both endpoint versions.",
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
      "text": "Commit the selected link operation and both endpoint concurrency updates atomically.",
      "kind": "product",
      "entities": [
        {
          "entity": "relation",
          "effect": "changes",
          "facts": [
            "Deleted at",
            "Deleted by",
            "Version",
            "Source version",
            "Target version"
          ],
          "from": "Deleted",
          "to": "Active"
        },
        {
          "entity": "issue",
          "as": "source-issue",
          "effect": "changes",
          "facts": [
            "Version",
            "Updated at"
          ]
        },
        {
          "entity": "issue",
          "as": "target-issue",
          "effect": "changes",
          "facts": [
            "Version",
            "Updated at"
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
      "target": "apps/worker/src/services/relations.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Restore relation agent primary

## Trigger

Request restoring the relationship with its own and both endpoint versions.

## Outcome

Relation 恢复

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Both endpoint versions and visibility are checked separately. Self or cross-Workspace relationships fail. Parent cycles and more than 1,000 checked objects fail without a new relation. Only related normalizes endpoints.
- This operation retains the idempotent-cas contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
- Either stale endpoint version or the stale link version refuses the entire write; neither endpoint is advanced alone.
