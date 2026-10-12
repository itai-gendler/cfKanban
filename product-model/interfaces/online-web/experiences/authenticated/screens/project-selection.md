---
{
  "entities": [
    {
      "entity": "web-session",
      "shows": [
        "Identity",
        "Principal",
        "Authentication source",
        "Target",
        "Allowed scope",
        "Entry",
        "Created at",
        "Activity at",
        "Expires at",
        "Absolute expiry",
        "Version",
        "Revoked at"
      ]
    },
    {
      "entity": "workspace",
      "shows": [
        "Identity",
        "Name"
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
      "target": "apps/web/src/components/ProjectSwitcher.vue"
    }
  ]
}
---

# Project selection

Explicit Project selection after fresh Session and access verification.

Current authorization is the effective Project/role and Session scope projection, not a direct-grant record inventory.
