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
    },
    {
      "entity": "instance",
      "verb": "owns",
      "cardinality": "one-to-one"
    }
  ]
}
---

# Owner

Instance Owner, still bound by authentication source and Session scope.
