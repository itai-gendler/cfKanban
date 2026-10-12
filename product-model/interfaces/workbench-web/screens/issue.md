---
{
  "entities": [
    {
      "entity": "issue",
      "shows": [
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
      "collects": [
        "Title",
        "Body",
        "Status",
        "Priority",
        "Assignee",
        "Labels",
        "Milestone"
      ]
    },
    {
      "entity": "comment",
      "shows": [
        "Identity",
        "Body",
        "Author",
        "Created at",
        "Reply target",
        "Version",
        "Deleted at",
        "Deleted by"
      ],
      "collects": [
        "Body",
        "Reply target"
      ]
    },
    {
      "entity": "completion-record",
      "shows": [
        "Identity",
        "Author",
        "Created at",
        "Summary",
        "Verification",
        "Artifacts",
        "Follow-ups"
      ],
      "collects": [
        "Summary",
        "Verification",
        "Artifacts",
        "Follow-ups"
      ]
    },
    {
      "entity": "principal",
      "shows": [
        "Identity",
        "Display name"
      ]
    },
    {
      "entity": "label",
      "shows": [
        "Identity",
        "Name",
        "Marker",
        "Version",
        "Deleted at",
        "Deleted by"
      ]
    },
    {
      "entity": "milestone",
      "shows": [
        "Identity",
        "Title",
        "Description",
        "Due date",
        "Status",
        "Version",
        "Progress"
      ]
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/embedded/Workbench.vue"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/local-runtime/src/workbench/controller.mjs"
    }
  ]
}
---

# Issue

Current task editing, commenting, completion and original-write recovery. Pending writes constrain later changes and rebinding.
