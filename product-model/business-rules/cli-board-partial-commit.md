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
      "type": "capability",
      "id": "create-board"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/workflows.mjs"
    }
  ]
}
---

# 两个原子操作，第一步不自动回滚

两个原子操作，第一步不自动回滚
