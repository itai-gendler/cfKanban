---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "principal"
    },
    {
      "type": "entity",
      "id": "credential"
    },
    {
      "type": "entity",
      "id": "project-grant"
    },
    {
      "type": "entity",
      "id": "workspace-administrator-grant"
    },
    {
      "type": "entity",
      "id": "project-administrator-grant"
    },
    {
      "type": "entity",
      "id": "issue"
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
      "target": "apps/worker/src/services/identity.ts"
    }
  ]
}
---

# 稳定 ID；改名不重绑历史

稳定 ID；改名不重绑历史
