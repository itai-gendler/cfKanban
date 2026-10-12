---
{
  "availability": [
    {
      "place": "online-web::authenticated"
    },
    {
      "place": "workbench-web"
    },
    {
      "place": "rest-api::authenticated"
    },
    {
      "place": "public-cli::authenticated"
    },
    {
      "place": "agent-skills::authenticated"
    },
    {
      "place": "mcp"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/project-members.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/principal-names.ts"
    }
  ]
}
---

# Browse assignees

合格身份的 ID/名称
