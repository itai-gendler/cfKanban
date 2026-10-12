---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "issue"
    },
    {
      "type": "entity",
      "id": "label"
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
      "target": "apps/worker/src/services/labels.ts"
    }
  ]
}
---

# 同 Project；最多 20 关联，删除定义保留关联并仍占关联计数

同 Project；最多 20 关联，删除定义保留关联并仍占关联计数

An Issue has at most twenty saved label associations. Deleting a label definition retains its associations and continues to consume their count.
