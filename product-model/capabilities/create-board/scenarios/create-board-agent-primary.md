---
{
  "kind": "primary",
  "routes": {
    "co": "Co entry"
  },
  "steps": [
    {
      "text": "Submit the container names for two sequential atomic creations.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "co": {
          "place": "public-cli::administration"
        }
      }
    },
    {
      "text": "Create the named top-level container and retain its independent result.",
      "kind": "product",
      "entities": [
        {
          "entity": "workspace",
          "effect": "creates",
          "facts": [
            "Identity",
            "Name",
            "Description",
            "Created at",
            "Updated at",
            "Version",
            "Archived at",
            "Archived by",
            "Trend history",
            "Trend coverage"
          ],
          "to": "Active"
        }
      ],
      "contexts": {
        "co": {
          "place": "public-cli::administration"
        }
      },
      "actor": "ai-agent"
    },
    {
      "text": "Create the named child under the committed parent and report the independent second result.",
      "kind": "product",
      "entities": [
        {
          "entity": "project",
          "effect": "creates",
          "facts": [
            "Identity",
            "Name",
            "Context",
            "Created at",
            "Updated at",
            "Version",
            "Archived at",
            "Archived by",
            "Trend history",
            "Trend coverage"
          ],
          "to": "Active"
        }
      ],
      "contexts": {
        "co": {
          "place": "public-cli::administration"
        }
      },
      "actor": "ai-agent"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/workflows.mjs"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Create board agent primary

## Trigger

Submit the container names for two sequential atomic creations.

## Outcome

CLI 顺序创建 Workspace、Project，分别报告结果

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
- The first committed container is not rolled back when the second creation is unconfirmed; each atomic result is retained.
