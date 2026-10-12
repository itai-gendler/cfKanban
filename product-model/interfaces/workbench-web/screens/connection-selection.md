---
{
  "entities": [
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
    },
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
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/embedded/Workbench.vue"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/local-runtime/src/workbench/controller.mjs"
    }
  ]
}
---

# Connection selection

Nonsecret connection candidates and verified Instance, Principal and scope selection.
