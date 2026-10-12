---
{
  "entities": [
    {
      "entity": "project",
      "shows": [
        "Identity",
        "Name",
        "Context",
        "Created at",
        "Updated at",
        "Version",
        "Archived at",
        "Archived by"
      ]
    },
    {
      "entity": "project-status-name",
      "shows": [
        "Project",
        "Status key",
        "Display name",
        "Category",
        "Position",
        "Terminal",
        "Project version"
      ]
    },
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

# Project

Currently bound Project, Board/List, limited filters and assignment, label and milestone choices.
