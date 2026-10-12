---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "comment",
      "effect": "changes",
      "facts": [
        "Body"
      ]
    }
  ],
  "permits": [],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/authorization.ts"
    }
  ]
}
---

# Nobody may change comment after it is saved

Comment changes：保存后的 Body

`permits: []`

Current data or management sources bind the selected Project; active parent checks and allowed Session scope remain mandatory. A fixed Project/Issue Session cannot acquire Instance management control. Relation endpoints are checked independently and both endpoint Rules must hold. The selected caller is bound to its explicit stable Principal. Management rights, data rights and browser scope are independently checked; Agent requests use their own Principal and never imply a human delegation.
