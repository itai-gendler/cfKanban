---
{
  "entities": [
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
    },
    {
      "entity": "recovery-invitation",
      "shows": [
        "Identity",
        "Bound principal",
        "Recovery mode",
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
      "target": "apps/web/src/App.vue"
    }
  ]
}
---

# Invitations

Project and recovery invitation management history, targets, mode, redemption and revocation.
