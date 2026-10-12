---
{
  "acts": "external",
  "kind": "person",
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/authorization.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/scoped-authorization.ts"
    }
  ],
  "relations": [
    {
      "entity": "principal",
      "verb": "is-identity-of",
      "cardinality": "one-to-one"
    }
  ]
}
---

# Participant

Authenticated person using their own identity settings; authentication alone grants no Project data access.
