---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "issue"
    },
    {
      "type": "entity",
      "id": "principal"
    },
    {
      "type": "entity",
      "id": "project-grant"
    },
    {
      "type": "entity",
      "id": "workspace-administrator-grant"
    },
    {
      "type": "entity",
      "id": "project-administrator-grant"
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
      "target": "apps/worker/src/services/principal-names.ts"
    }
  ]
}
---

# Owner/current Writer 合格，失权历史保留

A non-null assignee is the retained Owner Principal or a current effective writer in that same Project; a reader alone is not eligible. Clearing an assignee keeps writer authorization. Losing a source does not remove the historical assignee identity, but current eligibility and needs-reassignment projection change. Assignment creates no execution lock.
