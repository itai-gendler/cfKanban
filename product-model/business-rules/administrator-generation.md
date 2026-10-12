---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "workspace-administrator-grant"
    },
    {
      "type": "entity",
      "id": "project-administrator-grant"
    },
    {
      "type": "entity",
      "id": "project-invitation"
    },
    {
      "type": "entity",
      "id": "event"
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
      "target": "apps/worker/src/kernel/scoped-authorization.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/scoped-administrators.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/invitations.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "migrations/0009_scoped_administrators.sql"
    }
  ]
}
---

# 重授不复活旧 generation

Administrator revocation retains its source history. Regrant replaces generation, so an invitation retaining the previous administrator ID/generation remains invalid. Current management commits retain and recheck the resolved administrator source ID/generation and record its actual audit source.
