---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "issue"
    },
    {
      "type": "capability",
      "id": "browse-issues"
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

# 候选优先级/FIFO，普通列表另有顺序

Todo candidate queues use priority rank ascending, creation time ascending and issue number ascending. Ordinary active lists use updated time and number descending; deleted-only lists use deletion time and number descending. Browsing a candidate never assigns it.
