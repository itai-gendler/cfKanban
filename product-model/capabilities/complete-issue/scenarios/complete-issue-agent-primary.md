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
      "text": "Submit summary, verification, artifacts and follow-ups with the current version.",
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
      "text": "事项 Done，同时创建 Completion",
      "kind": "product",
      "entities": [
        {
          "entity": "issue",
          "effect": "changes",
          "facts": [
            "Status",
            "Version",
            "Updated at"
          ],
          "from": "In Progress",
          "to": "Done"
        },
        {
          "entity": "completion-record",
          "effect": "creates",
          "facts": [
            "Identity",
            "Author",
            "Created at",
            "Summary",
            "Verification",
            "Artifacts",
            "Follow-ups"
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
      "target": "apps/worker/src/services/comments.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    }
  ]
}
---

# Complete issue agent primary

## Trigger

Submit summary, verification, artifacts and follow-ups with the current version.

## Outcome

Issue Done，同时创建 Completion

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Canceled can complete. Blocking, another assignee or empty supplied verification do not themselves prevent completion. Already Done creates no duplicate record; reopening retains old completion evidence.
- This operation retains the idempotent-cas contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- On agent-skills::authenticated, mcp, 新完成记录，旧记录保留; affected saved facts: changes issue [Status, Version, Updated at]; creates completion record [Identity, Author, Created at, Summary, Verification, Artifacts, Follow-ups].

- On agent-skills::authenticated, mcp, Canceled 可完成; affected saved facts: changes issue [Status, Version, Updated at]; creates completion record [Identity, Author, Created at, Summary, Verification, Artifacts, Follow-ups].

- On agent-skills::authenticated, mcp, 不创建重复完成记录; affected saved facts: reads issue [Status, Version, Updated at].
