---
{
  "kind": "primary",
  "result": "achieved",
  "routes": {
    "wa": "WA hand-off"
  },
  "steps": [
    {
      "text": "Confirm soft deletion of the currently displayed work item with its current version.",
      "kind": "actor",
      "actor": "writer",
      "capability": "delete-issue",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::issue"
        }
      }
    },
    {
      "text": "Confirm the soft deletion before leaving the detail view.",
      "kind": "product",
      "actor": "writer",
      "capability": "delete-issue",
      "entities": [
        {
          "entity": "issue",
          "effect": "changes",
          "facts": [
            "Deleted at",
            "Deleted by",
            "Version",
            "Updated at"
          ]
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::issue"
        }
      }
    },
    {
      "text": "Navigate to the returned parent’s basic Board path and read its active work page.",
      "kind": "product",
      "actor": "writer",
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
        }
      }
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/views/IssueDetailView.vue"
    }
  ]
}
---

# Delete issue and return to board writer achieved

## Trigger

Delete work and return to its underlying Board.

## Outcome

Deletion is confirmed and the basic Board is displayed.

## Edge cases

- A refused or uncertain deletion does not assert a completed Board hand-off.
- A navigation or destination-read failure does not undo confirmed deletion. The basic Board return does not preserve the previous filters.
