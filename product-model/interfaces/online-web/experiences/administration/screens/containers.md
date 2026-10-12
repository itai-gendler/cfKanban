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
        "Archived by"
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

# Containers

Workspace and Project collection, creation, editing, archival and restoration.
