---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "notification",
      "effect": "changes",
      "facts": [
        "Title",
        "Body"
      ]
    }
  ],
  "permits": [],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/notifications.ts"
    }
  ]
}
---

# Nobody may change notification after it is saved

Notification changes：已发布 Title、Body

`permits: []`

The selected caller is bound to its explicit stable Principal. Management rights, data rights and browser scope are independently checked; Agent requests use their own Principal and never imply a human delegation.
