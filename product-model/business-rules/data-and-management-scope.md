---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "web-session"
    },
    {
      "type": "entity",
      "id": "project"
    },
    {
      "type": "entity",
      "id": "workspace"
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
      "target": "apps/worker/src/kernel/authorization.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/scoped-authorization.ts"
    }
  ]
}
---

# 数据、管理、scope 分开

Ordinary Project reader/writer access never implies manage_workspace, manage_project, manage_members or manage_administrators. Each management operation selects its own allowed source and Cookie scope. Instance Owner equality is separate from Owner control: fixed Project/Issue Cookie cannot acquire management control, while a matching Workspace Cookie has its established scoped management path.
