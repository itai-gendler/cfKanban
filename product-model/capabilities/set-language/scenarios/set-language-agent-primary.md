---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ca": "Ca entry",
    "sa": "Sa entry",
    "so": "So entry",
    "m": "M entry"
  },
  "steps": [
    {
      "text": "Choose en or zh-CN for the explicitly bound identity.",
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
        "so": {
          "place": "agent-skills::administration"
        },
        "m": {
          "place": "mcp"
        }
      }
    },
    {
      "text": "保存本人语言",
      "kind": "product",
      "entities": [
        {
          "entity": "principal",
          "effect": "changes",
          "facts": [
            "Preferred language",
            "Profile version",
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
        "so": {
          "place": "agent-skills::administration"
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
      "target": "apps/worker/src/services/identity.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    }
  ]
}
---

# Set language agent primary

## Trigger

Choose en or zh-CN for the explicitly bound identity.

## Outcome

保存本人语言

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- This operation retains the idempotent-cas contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
