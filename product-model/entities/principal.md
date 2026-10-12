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
      "target": "apps/worker/src/services/access.ts"
    }
  ],
  "relations": [
    {
      "entity": "credential",
      "verb": "has",
      "cardinality": "one-to-many"
    },
    {
      "entity": "passkey",
      "verb": "has",
      "cardinality": "one-to-many"
    },
    {
      "entity": "web-session",
      "verb": "has",
      "cardinality": "one-to-many"
    },
    {
      "entity": "project-grant",
      "verb": "has",
      "cardinality": "one-to-many"
    },
    {
      "entity": "workspace-administrator-grant",
      "verb": "has",
      "cardinality": "one-to-many"
    },
    {
      "entity": "project-administrator-grant",
      "verb": "has",
      "cardinality": "one-to-many"
    },
    {
      "entity": "recovery-invitation",
      "verb": "has",
      "cardinality": "one-to-many"
    },
    {
      "entity": "notification-preferences",
      "verb": "has",
      "cardinality": "one-to-one"
    },
    {
      "entity": "issue",
      "verb": "is-assigned",
      "cardinality": "one-to-many"
    },
    {
      "entity": "notification-acknowledgement",
      "verb": "has",
      "cardinality": "one-to-many"
    },
    {
      "entity": "attachment",
      "verb": "uploads",
      "cardinality": "one-to-many"
    },
    {
      "entity": "browser-launch",
      "verb": "creates",
      "cardinality": "one-to-many"
    },
    {
      "entity": "comment",
      "verb": "authors",
      "cardinality": "one-to-many"
    },
    {
      "entity": "completion-record",
      "verb": "authors",
      "cardinality": "one-to-many"
    },
    {
      "entity": "notification",
      "verb": "publishes",
      "cardinality": "one-to-many"
    }
  ]
}
---

# Principal

Stable identity shared across roles and interfaces. Names and preferences belong here; names never rebind history.

## Information kept

- **Identity** — Stable addressable identity.
- **Display name** — The display name of this principal, retained or disclosed with the object.
- **Preferred language** — Optional en or zh-CN preference; null retains the client’s fallback selection.
- **Appearance** — The saved orange or blue theme, independent of language.
- **Profile version** — Current concurrency version of display name, language and appearance preferences.
- **Created at** — Creation time retained with history.
- **Updated at** — Most recent persisted update time.
- **Credential count** — Derived count of unrevoked credentials for this stable identity.
- **Grant summary** — Management projection of the count of unrevoked direct grants; the detail operation separately returns a bounded grant inventory.
- **Assignment summary** — Derived management count of undeleted work items assigned to this stable identity, preserving assignment even after authorization is lost.
