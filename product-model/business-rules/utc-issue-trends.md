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
      "target": "apps/worker/src/services/issue-trends.ts"
    }
  ]
}
---

# UTC；默认 30、最多 365，当前日 partial

UTC；默认 30、最多 365，当前日 partial

Use UTC daily buckets, default thirty days and at most 365 days; present unknown history as null and the current day as partial.
