---
{
  "kind": "primary",
  "result": "achieved",
  "routes": {
    "b": "B hand-off"
  },
  "steps": [
    {
      "text": "Submit the new work item’s title, optional body and non-completed initial state in the verified working view.",
      "kind": "actor",
      "actor": "writer",
      "capability": "create-issue",
      "entities": [],
      "contexts": {
        "b": {
          "place": "workbench-web::project"
        }
      }
    },
    {
      "text": "Create the work item under the existing binding and obtain its confirmed identifier.",
      "kind": "product",
      "actor": "writer",
      "capability": "create-issue",
      "entities": [
        {
          "entity": "issue",
          "effect": "creates",
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
          ],
          "to": "Backlog"
        }
      ],
      "contexts": {
        "b": {
          "place": "workbench-web::project"
        }
      }
    },
    {
      "text": "Open and read the newly created work item’s detail using that returned identifier.",
      "kind": "product",
      "actor": "writer",
      "capability": "read-issue",
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
        "b": {
          "place": "workbench-web::issue"
        }
      }
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/local-runtime/src/workbench/controller.mjs"
    }
  ]
}
---

# Create issue and open detail writer achieved

## Trigger

Create work and continue directly in its detail.

## Outcome

The new work item is displayed in the detail the Product opens.

## Edge cases

- A refused creation does not open a new detail. An uncertain creation keeps its original pending request; confirmed readback can supply the new identifier.
- Failure to fetch detail retains the confirmed creation and its identity, without claiming rollback or a displayed detail.
