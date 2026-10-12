---
{
  "kind": "primary",
  "result": "achieved",
  "routes": {
    "wa": "WA hand-off",
    "b": "B hand-off"
  },
  "steps": [
    {
      "text": "Select a target from the freshly verified working-target menu.",
      "kind": "actor",
      "actor": "reader",
      "capability": "switch-project",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project-selection"
        },
        "b": {
          "place": "workbench-web::connection-selection"
        }
      }
    },
    {
      "text": "Verify the selected target and carry the same identity to its working view.",
      "kind": "product",
      "actor": "reader",
      "capability": "switch-project",
      "entities": [
        {
          "entity": "project",
          "effect": "reads",
          "facts": [
            "Identity",
            "Name"
          ]
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project"
        },
        "b": {
          "place": "workbench-web::project"
        }
      }
    },
    {
      "text": "Read the selected target’s work page after the verified navigation or local binding change.",
      "kind": "product",
      "actor": "reader",
      "capability": "browse-issues",
      "entities": [
        {
          "entity": "issue",
          "effect": "reads",
          "facts": [
            "Identity",
            "Identifier",
            "Title",
            "Body",
            "Status",
            "Priority",
            "Assignee",
            "Manual block reason",
            "Visible blocking",
            "Labels",
            "Milestone",
            "Created at",
            "Updated at",
            "Version",
            "Deleted at",
            "Deleted by"
          ]
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project"
        },
        "b": {
          "place": "workbench-web::project"
        }
      }
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/components/ProjectSwitcher.vue"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/local-runtime/src/workbench/controller.mjs"
    }
  ]
}
---

# Switch project and browse reader achieved

## Trigger

Change the verified work target and continue in its task view.

## Outcome

The new target is verified and its task view is displayed.

## Edge cases

- A failed target verification does not assert the new view. Pending local writes or changed local session context block rebinding and keep the original operation.
- Online switching refreshes the current browser scope before offering destinations. A selected destination never expands that scope.
