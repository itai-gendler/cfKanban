---
{
  "entities": [
    {
      "entity": "project-invitation",
      "shows": [
        "Project targets",
        "Roles",
        "Expires at"
      ]
    },
    {
      "entity": "recovery-invitation",
      "shows": [
        "Bound principal",
        "Recovery mode",
        "Expires at"
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

# Invitation review

Invitation target, roles, recovery mode and validity preview without consumption.
