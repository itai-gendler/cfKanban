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
      "text": "Request closing the selected target with its current version.",
      "kind": "actor",
      "actor": "writer",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project"
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
      "text": "里程碑 Closed",
      "kind": "product",
      "entities": [
        {
          "entity": "milestone",
          "effect": "changes",
          "facts": [
            "Status",
            "Version"
          ],
          "from": "Open",
          "to": "Closed"
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project"
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
      "target": "apps/worker/src/services/milestones.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    }
  ]
}
---

# Close milestone primary

## Trigger

Request closing the selected target with its current version.

## Outcome

Milestone Closed

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Same-Project Closed targets remain associable; closing does not complete work. Progress excludes deleted tasks and separates Done, Canceled and unfinished.
- This operation retains the cas contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- The existing milestone edit is CAS-only; a replay is not an idempotent result lookup and MCP supplies no idempotency key.
