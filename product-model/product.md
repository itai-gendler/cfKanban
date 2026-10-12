---
{
  "id": "cfkanban",
  "summary": "Self-hosted Kanban for people and agents using stable identities, scoped access and atomic work operations.",
  "category": "task-management",
  "tags": [
    "kanban",
    "collaboration",
    "self-hosted"
  ],
  "license": "MIT",
  "languages": [
    "en",
    "zh-CN"
  ],
  "limitations": [
    "Board is a Project working view, without an independent business identity.",
    "Workflow keys are fixed; renaming their display names adds no state.",
    "Ordinary creation and editing cannot enter Done; completion saves an immutable completion record.",
    "Assignment does not reserve exclusive execution rights.",
    "Management authority, data access and Session scope are checked separately.",
    "D1 holds core business facts; attachment content uses optional storage.",
    "CLI Board creation is two atomic operations and can partially complete."
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/App.vue"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/issues.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/workflows.mjs"
    }
  ]
}
---

# cfKanban

Workspace, Project and Issue organize work for people and agents. Stable Principal identities, scoped grants and atomic task transitions support assignment, comments, completion evidence, relations, labels, milestones, UTC trends, notifications and optional attachments. Online Web, REST, public CLI, Skills, MCP and the shared human Workbench have their own established entry and recovery contracts.
