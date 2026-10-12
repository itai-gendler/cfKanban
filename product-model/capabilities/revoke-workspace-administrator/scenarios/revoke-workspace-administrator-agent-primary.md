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
      "text": "Request revoking the selected scoped management source with its current version.",
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
      "text": "实例所有者 撤销 工作区 admin grant",
      "kind": "product",
      "entities": [
        {
          "entity": "workspace-administrator-grant",
          "effect": "changes",
          "facts": [
            "Revoked at",
            "Revoked by",
            "Version"
          ],
          "from": "Active",
          "to": "Revoked"
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
      "target": "apps/worker/src/services/scoped-administrators.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Revoke workspace administrator agent primary

## Trigger

Request revoking the selected scoped management source with its current version.

## Outcome

Owner 撤销 Workspace admin grant

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- This operation retains the idempotent-cas-delete contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
