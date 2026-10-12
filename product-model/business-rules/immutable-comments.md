---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "comment"
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
      "target": "apps/worker/src/services/comments.ts"
    }
  ]
}
---

# 正文 append-only

Standard comment bodies and completion payloads are append-only. A standard comment may be soft-deleted or restored with its own version; completion records expose only read and cannot use those mutations.
