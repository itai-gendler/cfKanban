---
{
  "kind": "primary",
  "result": "achieved",
  "routes": {
    "wo": "WO hand-off"
  },
  "steps": [
    {
      "text": "Select a target from the freshly verified working-target menu.",
      "kind": "actor",
      "actor": "owner",
      "capability": "switch-project",
      "entities": [],
      "contexts": {
        "wo": {
          "place": "online-web::administration::instance"
        }
      }
    },
    {
      "text": "Verify the selected target and carry the same identity to its working view.",
      "kind": "product",
      "actor": "owner",
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
        "wo": {
          "place": "online-web::authenticated::project"
        }
      }
    },
    {
      "text": "Read the selected target’s work page after the verified navigation or local binding change.",
      "kind": "product",
      "actor": "owner",
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
        "wo": {
          "place": "online-web::authenticated::project"
        }
      }
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/components/ProjectSwitcher.vue"
    }
  ]
}
---

# Switch project and browse owner achieved

## Trigger

Change the verified work target and continue in its task view.

## Outcome

The new target is verified and its task view is displayed.

## Edge cases

- A failed target verification does not assert the new view. Pending local writes or changed local session context block rebinding and keep the original operation.
- Online switching refreshes the current browser scope before offering destinations. A selected destination never expands that scope.
