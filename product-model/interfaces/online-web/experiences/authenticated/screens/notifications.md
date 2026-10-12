---
{
  "entities": [
    {
      "entity": "notification",
      "shows": [
        "Identity",
        "Title",
        "Body",
        "Publisher",
        "Published at",
        "Expires at",
        "Withdrawn at",
        "Version",
        "Visible status"
      ],
      "collects": [
        "Title",
        "Body",
        "Expires at"
      ]
    },
    {
      "entity": "notification-acknowledgement",
      "shows": [
        "Notification",
        "Principal",
        "Acknowledged at"
      ]
    },
    {
      "entity": "notification-preferences",
      "shows": [
        "Principal",
        "Enabled",
        "Receive after",
        "Version"
      ],
      "collects": [
        "Enabled"
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

# Notifications

Notice history, pending notices, explicit acknowledgements, reception settings and source-appropriate publishing.
