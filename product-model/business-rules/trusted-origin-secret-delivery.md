---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "credential"
    },
    {
      "type": "entity",
      "id": "browser-launch"
    },
    {
      "type": "entity",
      "id": "project-invitation"
    },
    {
      "type": "entity",
      "id": "recovery-invitation"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/issues.ts"
    }
  ]
}
---

# 私有状态、可信 origin、秘密不进入普通输出

私有状态、可信 origin、秘密不进入普通输出
