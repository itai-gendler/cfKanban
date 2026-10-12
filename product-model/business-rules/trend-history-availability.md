---
{
  "appliesTo": [
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
      "target": "apps/worker/src/services/issue-trends.ts"
    }
  ]
}
---

# 未知 null；Workspace 最多 100 active Projects

未知 null；Workspace 最多 100 active Projects

Workspace aggregation includes every active Project and refuses more than one hundred, rather than publishing a partial visible subset as complete.
