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

# Parent 不成环，包括检查涉及的历史对象

Parent 不成环，包括检查涉及的历史对象

These graph validation gates apply to proposed Parent creation/restoration; deleting a link does not require a successful new Parent traversal. Relevant historical endpoint objects remain part of the implemented traversal, rather than a blanket guarantee that all deleted relations are traversed.
