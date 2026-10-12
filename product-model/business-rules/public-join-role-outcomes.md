---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "public-join-policy"
    },
    {
      "type": "entity",
      "id": "project-grant"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/public-join.ts"
    }
  ]
}
---

# 新建、重授、升级分开；不降级 Writer

新建、重授、升级分开；不降级 Writer
