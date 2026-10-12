---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "workspace"
    },
    {
      "type": "entity",
      "id": "project"
    },
    {
      "type": "entity",
      "id": "issue"
    },
    {
      "type": "entity",
      "id": "comment"
    },
    {
      "type": "entity",
      "id": "relation"
    },
    {
      "type": "entity",
      "id": "attachment"
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/containers.ts"
    }
  ]
}
---

# 活跃父容器与恢复例外分别处理

Ordinary data source effectiveness and ordinary disclosure require active Project and Workspace parents. Archived Workspace recovery inventory is Owner control. Archived Project recovery/management exceptions are operation-specific Owner/Workspace administrator paths; Project administrator cannot survive archival. The deleted-child recovery view may retain its explicit Owner-only parent exception, while ordinary writer sources remain ineffective under archived parents. Retained grants and assignment history are not destroyed by container archival.
