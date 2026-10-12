---
{
  "appliesTo": [
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
    },
    {
      "type": "entity",
      "id": "project"
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
      "target": "migrations/0009_scoped_administrators.sql"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/authorization.ts"
    }
  ]
}
---

# 当前来源合并；较强角色生效

Use project_access_sources/effective_project_grants for direct and scoped-administrator sources. An active direct reader/writer source is independent from inherited writer sources; writer takes precedence, with Workspace administrator before Project administrator before direct source at equal role. Revocation removes only that source. Active parents and live Session intersection remain separate checks.
