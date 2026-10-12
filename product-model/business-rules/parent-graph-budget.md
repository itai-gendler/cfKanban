---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "relation"
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
      "target": "apps/worker/src/services/relations.ts"
    }
  ]
}
---

# 超过 1,000 检查预算拒绝

超过 1,000 检查预算拒绝

Parent validation stops at the established 1,000-object budget and refuses the mutation when validation cannot complete.

These graph validation gates apply to proposed Parent creation/restoration; deleting a link does not require a successful new Parent traversal. Relevant historical endpoint objects remain part of the implemented traversal, rather than a blanket guarantee that all deleted relations are traversed.
