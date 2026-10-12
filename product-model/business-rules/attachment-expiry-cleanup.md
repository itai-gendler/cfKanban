---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "attachment",
      "effect": "changes",
      "facts": [
        "Budget released at"
      ]
    }
  ],
  "permits": [
    {
      "unattended": true
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/attachments.ts"
    }
  ]
}
---

# Only bounded validated Product maintenance releases attachment reservation budget (change Attachment Budget released at)

Unattended maintenance selects tracked expired/deleted reservations, rechecks current object state, performs or confirms content removal/head and preserves late-upload safety before marking budget released. Expired timestamps alone do not release bytes. This operation has no human or AI request-Principal precondition.
