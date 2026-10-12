---
{
  "kind": "primary",
  "routes": {
    "wo": "Wo entry",
    "ro": "Ro entry",
    "co": "Co entry"
  },
  "steps": [
    {
      "text": "Submit a nonempty display name for a fixed workflow key with the current parent version; resetting sends the shipped default name.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wo": {
          "place": "online-web::administration::containers"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        }
      }
    },
    {
      "text": "Save the display name and advance its parent concurrency version in one atomic commit.",
      "kind": "product",
      "entities": [
        {
          "entity": "project-status-name",
          "effect": "changes",
          "facts": [
            "Display name",
            "Project version"
          ],
          "from": "Default",
          "to": "Renamed"
        },
        {
          "entity": "project",
          "effect": "changes",
          "facts": [
            "Version",
            "Updated at"
          ]
        }
      ],
      "contexts": {
        "wo": {
          "place": "online-web::administration::containers"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        }
      },
      "actor": "owner"
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

# Rename project status name owner primary

## Trigger

Submit a nonempty display name for a fixed workflow key with the current parent version; resetting sends the shipped default name.

## Outcome

修改固定状态的显示名称

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- This operation retains the cas contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
- The fixed key, category, position and terminal property do not change. Empty API names are invalid; a reset supplies the default display name.
