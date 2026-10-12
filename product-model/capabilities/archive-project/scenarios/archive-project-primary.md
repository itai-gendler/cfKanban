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
      "text": "Confirm archival of the selected child container with its current version; the service records the time and acting identity.",
      "kind": "actor",
      "actor": "workspace-administrator",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::workspace"
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
      "text": "项目 归档",
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
          "from": "Active",
          "to": "Archived"
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::workspace"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      },
      "actor": "workspace-administrator"
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

# Archive project primary

## Trigger

Confirm archival of the selected child container with its current version; the service records the time and acting identity.

## Outcome

Project 归档

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- This operation retains the cas-delete contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
