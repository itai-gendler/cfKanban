---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ca": "Ca entry",
    "sa": "Sa entry",
    "m": "M entry"
  },
  "steps": [
    {
      "text": "Choose kind, explicit endpoint identities and both endpoint versions.",
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
        },
        "m": {
          "place": "mcp"
        }
      }
    },
    {
      "text": "Commit the selected link operation and both endpoint concurrency updates atomically.",
      "kind": "product",
      "entities": [
        {
          "entity": "relation",
          "effect": "creates",
          "facts": [
            "Identity",
            "Kind",
            "Source",
            "Target",
            "Source version",
            "Target version",
            "Version",
            "Deleted at",
            "Deleted by"
          ],
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
        },
        "m": {
          "place": "mcp"
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
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    }
  ]
}
---

# Add relation agent primary

## Trigger

Submit relation kind and both endpoint identities and versions.

## Outcome

新 Relation

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Both endpoint versions and visibility are checked separately. Self or cross-Workspace relationships fail. Parent cycles and more than 1,000 checked objects fail without a new relation. Only related normalizes endpoints.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- On agent-skills::authenticated, mcp, 超过 1,000 检查预算拒绝; this boundary adds no confirmed saved mutation.

- On agent-skills::authenticated, mcp, 拒绝形成 Parent 环; this boundary adds no confirmed saved mutation.
- Either stale endpoint version or the stale link version refuses the entire write; neither endpoint is advanced alone.
