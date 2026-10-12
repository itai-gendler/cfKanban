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

# Reader

Person with a current Project reading source.
