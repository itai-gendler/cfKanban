---
{
  "entities": [
    {
      "entity": "principal",
      "shows": [
        "Identity",
        "Display name"
      ]
    },
    {
      "entity": "project-invitation",
      "shows": [
        "Project targets",
        "Roles",
        "Expires at"
      ]
    },
    {
      "entity": "project-grant",
      "shows": [
        "Project",
        "Role"
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

# Authenticated invitation

Invitation preview and acceptance by the current identity.
