---
{
  "entities": [
    {
      "entity": "attachment-capacity",
      "shows": [
        "Configured",
        "Limit",
        "Reserved bytes",
        "Version"
      ],
      "collects": [
        "Limit"
      ]
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/components/AttachmentStorageSettings.vue"
    }
  ]
}
---

# Attachment capacity

Independent attachment configuration, byte limit, reserved budget and version.
