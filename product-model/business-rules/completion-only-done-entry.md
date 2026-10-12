---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "issue"
    },
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

# Done 使用完成操作

Ordinary creation and update reject Done as a destination. The dedicated complete operation enters Done with its completion record; reopening leaves Done for a selected non-Done state while retaining past completion history.
