---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "principal"
    },
    {
      "type": "entity",
      "id": "project"
    },
    {
      "type": "context",
      "context": {
        "place": "workbench-web"
      }
    },
    {
      "type": "capability",
      "id": "open-workbench"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/local-runtime/src/workbench/controller.mjs"
    }
  ]
}
---

# 核验绑定、清除旧数据、pending 阻止切换/新写入

Explicit selection verifies instance, stable identity and working target. Changing the binding clears old view data. Pending operations or a changed source session block a new mutation/rebind; recoveries retain their original binding, request, expected version and key. Responses for another identity are not merged into the current profile.
