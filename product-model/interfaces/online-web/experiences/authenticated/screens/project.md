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
        "Archived by",
        "Trend history",
        "Trend coverage"
      ]
    },
    {
      "entity": "workspace",
      "shows": [
        "Identity",
        "Name",
        "Description",
        "Created at",
        "Updated at",
        "Version",
        "Archived at",
        "Archived by"
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
    },
    {
      "entity": "principal",
      "shows": [
        "Identity",
        "Display name"
      ]
    },
    {
      "entity": "event",
      "shows": [
        "Identity",
        "Sequence",
        "Stream",
        "Operation",
        "Actor principal",
        "Actor credential",
        "Authorized via",
        "Workspace",
        "Project",
        "Subject",
        "Payload",
        "Created at"
      ]
    },
    {
      "entity": "project-grant",
      "shows": [
        "Identity",
        "Principal",
        "Project",
        "Role",
        "Version",
        "Granted at",
        "Revoked at"
      ]
    },
    {
      "entity": "project-administrator-grant",
      "shows": [
        "Identity",
        "Principal",
        "Project",
        "Workspace",
        "Version",
        "Generation",
        "Granted at",
        "Revoked at"
      ]
    },
    {
      "entity": "project-invitation",
      "shows": [
        "Identity",
        "Project targets",
        "Roles",
        "Expires at",
        "Version",
        "Redeemed at",
        "Redeemed by",
        "Revoked at"
      ]
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/views/ProjectBoardView.vue"
    }
  ]
}
---

# Project

Selected Project Board/List, state names, labels, milestones, activity, trends and applicable scoped management.
