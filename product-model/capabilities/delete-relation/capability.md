---
{
  "availability": [
    {
      "place": "online-web::authenticated"
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
      "target": "apps/worker/src/services/relations.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "contracts/openapi.json"
    }
  ]
}
---

# Delete relation

Relation 软删除
