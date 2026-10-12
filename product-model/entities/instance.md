---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/identity.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/auth.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "migrations/0001_initial.sql"
    }
  ],
  "relations": [
    {
      "entity": "workspace",
      "verb": "contains",
      "cardinality": "one-to-many"
    },
    {
      "entity": "principal",
      "verb": "contains",
      "cardinality": "one-to-many"
    },
    {
      "entity": "notification",
      "verb": "contains",
      "cardinality": "one-to-many"
    },
    {
      "entity": "attachment-capacity",
      "verb": "has",
      "cardinality": "one-to-one"
    },
    {
      "entity": "homepage-settings",
      "verb": "has",
      "cardinality": "one-to-one"
    },
    {
      "entity": "principal",
      "verb": "is-owned-by",
      "cardinality": "one-to-one"
    }
  ],
  "singleton": true
}
---

# Instance

Public discovery and verified connection identity with advertised service information.

## Information kept

- **Identity** — Stable addressable identity.
- **Release version** — Shipped release_version returned by discovery and authenticated metadata, displayed by the public footer and Owner summary.
- **Service version** — The service version of this instance, retained or disclosed with the object.
- **Schema version** — The schema version of this instance, retained or disclosed with the object.
- **Discovery version** — The discovery version of this instance, retained or disclosed with the object.
- **Observed origin** — The observed origin of this instance, retained or disclosed with the object.
- **Preferred origin** — The preferred origin of this instance, retained or disclosed with the object.
- **Origin version** — The origin version of this instance, retained or disclosed with the object.
- **Advertised capabilities** — The advertised capabilities of this instance, retained or disclosed with the object.

- **Owner principal** — The unique retained owner_principal_id used for request Principal equality, not an anonymous discovery field.
