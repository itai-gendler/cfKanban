---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ro": "Ro entry",
    "ca": "Ca entry",
    "co": "Co entry",
    "sa": "Sa entry",
    "so": "So entry"
  },
  "steps": [
    {
      "text": "Request restoration of the archived child container with its current version.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
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
      "text": "项目 恢复",
      "kind": "product",
      "entities": [
        {
          "entity": "project",
          "effect": "changes",
          "facts": [
            "Archived at",
            "Archived by",
            "Version",
            "Updated at"
          ],
          "from": "Archived",
          "to": "Active"
        }
      ],
      "contexts": {
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
      "target": "apps/worker/src/services/containers.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Restore project agent primary

## Trigger

Request restoration of the archived child container with its current version.

## Outcome

Project 恢复

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- This operation retains the idempotent-cas contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
