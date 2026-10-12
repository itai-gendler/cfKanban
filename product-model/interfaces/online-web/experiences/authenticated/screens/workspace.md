---
{
  "entities": [
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
        "Archived by",
        "Trend history",
        "Trend coverage"
      ]
    },
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
      "entity": "workspace-administrator-grant",
      "shows": [
        "Identity",
        "Principal",
        "Workspace",
        "Version",
        "Generation",
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
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/views/ScopedManagementView.vue"
    }
  ]
}
---

# Workspace

Selected Workspace, its Projects, archival and management information, and all-active-Project aggregate trends.
