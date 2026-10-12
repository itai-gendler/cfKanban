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
      "entity": "public-join-policy",
      "shows": [
        "Public identity",
        "Summary",
        "Allowed roles"
      ]
    },
    {
      "entity": "instance",
      "shows": [
        "Identity",
        "Service version",
        "Schema version",
        "Discovery version",
        "Observed origin",
        "Preferred origin",
        "Origin version",
        "Advertised capabilities"
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

# Authenticated home

Own identity, visible Projects and public-join offers.
