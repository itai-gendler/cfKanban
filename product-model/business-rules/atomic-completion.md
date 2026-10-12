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
    },
    {
      "type": "capability",
      "id": "complete-issue"
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

# 状态与记录原子产生

The complete operation advances the work item into Done and appends one immutable completion record in the same atomic commit, under the current version. Conflict or refusal creates neither an isolated completion record nor a Done transition.
