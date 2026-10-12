---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "completion-record"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/issues.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/comments.ts#completeIssue"
    }
  ]
}
---

# 保存输入及默认值，不生成验证结果

Summary, verification, artifacts and follow-ups are caller input with the implemented defaults. Persisting verification text does not establish that any test or verification was run by the Product.
