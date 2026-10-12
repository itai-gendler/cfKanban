---
{
  "kind": "primary",
  "routes": {
    "wa": "Wa entry",
    "b": "B entry",
    "ra": "Ra entry",
    "ca": "Ca entry"
  },
  "steps": [
    {
      "text": "Submit summary, verification, artifacts and follow-ups with the current version.",
      "kind": "actor",
      "actor": "writer",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::issue"
        },
        "b": {
          "place": "workbench-web::issue"
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
      "text": "新完成记录，旧记录保留",
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
          "from": "Todo",
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
        "wa": {
          "place": "online-web::authenticated::issue"
        },
        "b": {
          "place": "workbench-web::issue"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      },
      "actor": "writer"
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

# Complete issue complete after reopen

## Trigger

Submit summary, verification, artifacts and follow-ups with the current version.

## Outcome

新完成记录，旧记录保留

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Canceled can complete. Blocking, another assignee or empty supplied verification do not themselves prevent completion. Already Done creates no duplicate record; reopening retains old completion evidence.
- This operation retains the idempotent-cas contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
