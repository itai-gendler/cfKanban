---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "attachment"
    },
    {
      "type": "entity",
      "id": "attachment-capacity"
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

# 有界删除/head 验证后释放，保留迟到写入防护

Tracked expired Pending objects become garbage. Bounded reclamation deletes content and confirms absence with head before reducing reserved bytes once; failure retains the budget. Permanent tombstones permit later deletion of delayed writes. Cleanup does not advance attachment metadata version.
