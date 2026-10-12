---
{
  "entities": [
    {
      "entity": "principal",
      "shows": [
        "Identity",
        "Display name",
        "Preferred language",
        "Appearance",
        "Profile version",
        "Created at",
        "Updated at"
      ],
      "collects": [
        "Display name",
        "Preferred language",
        "Appearance"
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

# Profile

Own profile, language, Appearance and Passkey inventory.
