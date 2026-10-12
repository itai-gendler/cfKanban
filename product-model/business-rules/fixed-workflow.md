---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "issue"
    },
    {
      "type": "entity",
      "id": "project-status-name"
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

# 五个 key 固定

The five status keys are backlog, todo, in_progress, done and canceled. Renaming a Project display name leaves keys, ordering, categories and terminal properties unchanged; no custom state is added.
