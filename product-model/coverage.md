---
{
  "scope": "Pinned-source online Kanban, scoped management, identity/access, collaboration, settings, public CLI/Skills/MCP and shared Workbench task contracts.",
  "method": "Read-only static inventory and entry-to-handler, persistence and authorization inspection at 7bb4d0758441932769039e63d18cf1c2f3158ffd.",
  "covered": [
    {
      "description": "Online entry, Board/detail navigation and directly traced subject views and controls.",
      "paths": [
        "apps/web/src/App.vue",
        "apps/web/src/components/ProjectSwitcher.vue",
        "apps/web/src/components/ScopedInvitations.vue",
        "apps/web/src/components/HomepageSettingsPanel.vue",
        "apps/web/src/components/AttachmentStorageSettings.vue",
        "apps/web/src/views/ProjectBoardView.vue",
        "apps/web/src/views/IssueDetailView.vue",
        "apps/web/src/views/ScopedManagementView.vue",
        "apps/web/src/views/IssueTrendsView.vue",
        "apps/web/src/views/PublicHomeView.vue",
        "apps/web/src/views/NotificationsView.vue"
      ]
    },
    {
      "description": "Shared task-view and binding controller paths, limited to established task operations and pending recovery.",
      "paths": [
        "apps/web/src/embedded/",
        "packages/local-runtime/src/workbench/"
      ]
    },
    {
      "description": "Core container/task/collaboration services and their scoped authorization guards.",
      "paths": [
        "apps/worker/src/services/containers.ts",
        "apps/worker/src/services/issues.ts",
        "apps/worker/src/services/comments.ts",
        "apps/worker/src/services/relations.ts",
        "apps/worker/src/services/labels.ts",
        "apps/worker/src/services/milestones.ts",
        "apps/worker/src/services/issue-trends.ts",
        "apps/worker/src/kernel/authorization.ts",
        "apps/worker/src/kernel/scoped-authorization.ts"
      ]
    },
    {
      "description": "Identity, grants, invitation, join and browser authentication service paths.",
      "paths": [
        "apps/worker/src/services/identity.ts",
        "apps/worker/src/services/access.ts",
        "apps/worker/src/services/project-members.ts",
        "apps/worker/src/services/scoped-administrators.ts",
        "apps/worker/src/services/invitations.ts",
        "apps/worker/src/services/public-join.ts",
        "apps/worker/src/services/web-auth.ts",
        "apps/worker/src/services/web-session-renewal.ts",
        "apps/worker/src/services/passkeys.ts",
        "apps/worker/src/kernel/auth.ts",
        "apps/worker/src/services/web-session-state.ts",
        "apps/worker/src/services/public-join-sql.ts",
        "apps/worker/src/services/principal-names.ts"
      ]
    },
    {
      "description": "Attachment/settings, homepage, notifications and user-visible event service paths.",
      "paths": [
        "apps/worker/src/services/attachments.ts",
        "apps/worker/src/services/attachment-settings.ts",
        "apps/worker/src/services/homepage-settings.ts",
        "apps/worker/src/services/notifications.ts",
        "apps/worker/src/services/events.ts",
        "apps/worker/src/services/notification-pending-cache.ts"
      ]
    },
    {
      "description": "Public CLI business catalog, dispatch and traced Board/join/recovery workflows.",
      "paths": [
        "packages/cli/src/catalog.mjs",
        "packages/cli/src/main.mjs",
        "packages/cli/src/parser.mjs",
        "packages/cli/src/runtime.mjs",
        "packages/cli/src/workflows.mjs"
      ]
    },
    {
      "description": "Installed Skills business facade, secure operation delivery and attachment transport paths.",
      "paths": [
        "packages/skill-runtime/src/mcp-facade.mjs",
        "packages/skill-runtime/src/transport.mjs",
        "packages/skill-runtime/src/credential-operations.mjs",
        "packages/skill-runtime/src/attachments.mjs"
      ]
    },
    {
      "description": "MCP public facade/opener registration and app-only routing boundary.",
      "paths": [
        "packages/mcp/src/server.mjs",
        "packages/mcp/src/workbench.mjs"
      ]
    },
    {
      "description": "Related HTTP operation definitions and inspected core/scoped-grant/settings/session/milestone/trend persistence definitions.",
      "paths": [
        "contracts/openapi.json",
        "migrations/"
      ]
    }
  ],
  "exclusions": [
    {
      "description": "Styling, icons and presentation-only assets.",
      "paths": [
        "apps/web/src/assets/",
        "images/"
      ]
    },
    {
      "description": "Engineering test harnesses, CI and build/generation validation machinery.",
      "paths": [
        "scripts/tests/",
        ".github/"
      ]
    }
  ],
  "unmapped": [
    {
      "description": "Complete purge, Owner-device/recovery, usage/history/control and release-update services.",
      "paths": [
        "apps/worker/src/services/container-purge.ts",
        "apps/worker/src/services/owner-devices.ts",
        "apps/worker/src/services/usage.ts",
        "apps/worker/src/services/usage-history.ts",
        "apps/worker/src/services/cloudflare-control.ts",
        "apps/worker/src/services/release-updates.ts",
        "apps/worker/src/services/upgrade-notifications.ts"
      ]
    },
    {
      "description": "Complete install/deploy/upgrade/rollback, artifact trust, host tooling, rebind and journal lifecycles.",
      "paths": [
        "packages/skill-runtime/src/deployment-finalize.mjs",
        "packages/skill-runtime/src/instance-upgrade.mjs",
        "packages/skill-runtime/src/owner-recovery.mjs",
        "packages/skill-runtime/src/rebind.mjs",
        "packages/skill-runtime/src/journal.mjs",
        "release/",
        "skills/"
      ]
    },
    {
      "description": "Search index, mentions, cache synchronization and cache access revocation.",
      "paths": [
        "apps/worker/src/services/search-index.ts",
        "packages/mcp/src/mentions.mjs",
        "packages/mcp/src/search-cache.mjs",
        "packages/mcp/src/search-cache-worker.mjs"
      ]
    },
    {
      "description": "Complete remembered/default MCP target, view persistence/release, DSH host lifecycle and local broker registry/delivery.",
      "paths": [
        "packages/mcp/src/workbench-preferences.mjs",
        "packages/dsh-plugin/",
        "packages/local-runtime/src/server.mjs"
      ]
    },
    {
      "description": "Trend projection/backfill maintenance beyond observed trend reading.",
      "paths": [
        "apps/worker/src/services/issue-trend-projection.ts",
        "packages/skill-runtime/src/issue-trend-backfill.mjs"
      ]
    },
    {
      "description": "Documentation-site browsing and other untraced public-content behavior.",
      "paths": [
        "apps/docs/"
      ]
    }
  ],
  "limitations": []
}
---

# Coverage
