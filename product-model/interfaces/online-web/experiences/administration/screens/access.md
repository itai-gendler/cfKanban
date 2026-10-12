---
{
  "entities": [
    {
      "entity": "principal",
      "shows": [
        "Identity",
        "Display name",
        "Profile version",
        "Created at",
        "Updated at",
        "Credential count",
        "Grant summary",
        "Assignment summary"
      ]
    },
    {
      "entity": "credential",
      "shows": [
        "Identity",
        "Principal",
        "Fingerprint",
        "Device name",
        "Created at",
        "Last used at",
        "Revoked at",
        "Revocation reason",
        "Version"
      ]
    },
    {
      "entity": "passkey",
      "shows": [
        "Identity",
        "Principal",
        "Authenticator description",
        "Created at",
        "Last used at",
        "Version",
        "Revoked at"
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

# Access

Identity management, nonsecret authenticators, access sources and non-Owner recovery targets.
