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
      ]
    },
    {
      "entity": "project",
      "shows": [
        "Identity",
        "Name"
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
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/App.vue"
    }
  ]
}
---

# Work list

Bounded work list across explicitly selected one to twenty Projects.
